<template>
  <div class="header">
    <div class="header__logo">
      <router-link to="/" class="header__logo--img">
        <img src="@/assets/images/logo.png" alt="">
        <span class="blind">logo</span>
      </router-link>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Header'
}
</script>
