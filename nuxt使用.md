[toc]
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

## this指向
服务器端:this -> undefined
客户端:this -> 组件本身

## nuxtServerInit

在store中,一般会做初始化
```
export const actions ={
    nuxtServerInit(store,context){
        console.log(store,context)
    }
}
```
## middleware

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

## validate
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
## asyncData & fetch
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
