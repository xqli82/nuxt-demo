# 1.Nuxt生命周期
request -> nuxtServerInit -> middleware -> validate() -> asyncData & fetch() -> render -> vue周期(客户端)

运行在服务器的钩子:
+ nuxtServerInit 
+ middleware
+ validate
+ asyncData & fetch

** 服务器端的钩子拿不到客户端的数据 **

注意:beforeCreate 和 create两个钩子,会运行在服务端和客户端;

运行在客户端的钩子:
+ beforeMounte
+ mounted
+ beforeUpdate
+ Updated
+ beforeDestroy
+ destroy

** 跑在客户端的钩子,都可以通过context访问到服务器端的数据 **

context包括:isDev, route, store, env, params, query, req, res, redirect, error

## 1.1 this指向
服务器端:this -> undefined
客户端:this -> 组件本身

## 1.2 nuxtServerInit

在store中,一般会做初始化
```
export const actions ={
    nuxtServerInit(store,context){
        console.log(store,context)
    }
}
```
## 1.3 middleware

1.全局设置
nuxt.config.js中定义router:
```
    router:{
        middleware:'auth'
    }
```
然后每次路由访问就会访问middleware文件夹下的auth.js文件

2.可以在页面层级中运行钩子
```
<script>
    export default {
        middleware:'auth', //页面层架的中间件
    }
</script>

//或者
<script>
    export default {
        middleware(){

        }
    }
</script>
```
3.中间件执行流程顺序

nuxt.config.js -> 匹配布局 -> 匹配页面

## 1.4 validate
+ 必须定义在页面组件
+ 主要校验信息
```
validate(context){
    //校验业务
    return true //or false
}

//或者
validate({params,query}){
    //校验业务
    return ture //or false
}
```
## 1.5 asyncData & fetch
+ asyncData 主要用于获取服务端的数据
```
asyncData(){
    //异步获取数据
    return{ //需要显示的return
        data1:1   //此处的data1会与data(){}中的数据合并,并最终渲染页面
    }
}
```
+ fetch 也可以获取异步数据,但是会将读取到的数据返回给vuex
```
fetch({store}){
    console.log('fetch')  //无需return
}
```
# 2.nuxt 路由
不需要配置路由,而通过pages下的文件自动生成路由

## 2.1路由级别
举例:
```
pages
--goods
----index.vue
----_id.vue
```  
index.vue为一级路由,_id为二级路由  
## 2.2路由跳转
```
<nuxt-link to='/goods'></nuxt-link>   
<nuxt-link to='/goods/1?a=1&b=2'></nuxt-link>   
<nuxt-link :to="{name:'goods-id',pararms:{id:3},query:{a:1,b:2}}">商品3</nuxt-link>   
//name: 路由名->其他目录->文件名
<nuxt/>
```
## 2.3 扩展型路由
在nuxt.config.js 的router项中配置
```
router:{
    //全局路由中间件
    middleware:'auth',
    //扩展路由
    extendRoutes(routes,resolve){
        routes.push({
            name:'root',
            path:'/index',
            component:resolve(__dirname,'pages/index.vue')
        })
    }
}
```
## 2.4目标路由参数校验
```
validate({params}){
    return true //or false
}
```
## 2.5错误页面
layout目录下创建error.vue
```
//error.vue

<template>
  <div class="container">
    <h1 v-if="error.statusCode">{{error.message}}</h1>
    <h1 v-else> 应用发生异常</h1>
    <button @click="$router.replace('/')">返回首页</button>
  </div>
</template>

<script>
export default {
    props:['error']
}
</script>

<style>

</style>

```

