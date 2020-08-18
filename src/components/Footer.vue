<template>
  <div class="footer">
    <div class="footer__inner">
      <router-link to="/" class="footer__inner--home">
        <b-icon icon="house-fill"></b-icon>
      </router-link>
      <router-link to="write" class="footer__inner--add">
        <b-icon icon="plus-square"></b-icon>
      </router-link>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Footer',
  props: {
  }
}
</script>
