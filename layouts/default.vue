<template>
  <div class="v5-container v5-color-bg-warning">
    <div class="blog-header v5-flex v5-flex-h-space-between v5-flex-v-center">
      <div class="box-box">LOGO</div>
      <div class="navigation-box">
        <nuxt-link to="/">
          <span>首页</span>
        </nuxt-link>
        <nuxt-link to="/about">
          <span>关于</span>
        </nuxt-link>
        <nuxt-link to="/link">
          <span>友链</span>
        </nuxt-link>

      </div>
      <div class="login-tips-text-box">登录 | 注销</div>
    </div>
    <Nuxt />
    <div class="footer-box">footer</div>
  </div>
</template>

<style>
  .blog-header{
    height: 50px;
  }
</style>
