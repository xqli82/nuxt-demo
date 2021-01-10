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
