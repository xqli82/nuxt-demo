<template>
  <div class="container">
    {{id}}
  </div>
</template>

<script>
export default {
    asyncData({isDev, route, store, env, params, query, req, res, redirect, error}) {
        return{
            id:params.id
        }
        
    },
}
</script>

<style>

</style>
