<template>
  <div class="v5-container v5-color-bg-white" id="main">
    <div
      class="blog-header v5-flex v5-flex-h-space-between v5-flex-v-center v5-color-white"
    >
      <div class="box-box">LOGO</div>
      <div class="navigation-box">
        <nuxt-link to="/" class="v5-inline-block v5-margin-r10">
          <span>首页</span>
        </nuxt-link>
        <nuxt-link to="/about">
          <span>关于</span>
        </nuxt-link>
        <nuxt-link to="/link">
          <span>友链</span>
        </nuxt-link>
        <nuxt-link to="/index">
          <span>index</span>
        </nuxt-link>
      </div>
      <div class="login-tips-text-box">登录 | 注销</div>
    </div>
    <Nuxt />
    <div class="footer-box v5-text-center">footer</div>
  </div>
</template>

<style>
.blog-header {
  height: 50px;
}
#main {
  height: 100vh;
  width: 100vw;
}
</style>
