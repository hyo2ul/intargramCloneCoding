<template>
  <div class="header">
    <div class="header__logo">
      <router-link to="/" class="header__logo--img">
        <img src="@/assets/images/logo.png" alt="">
        <span class="blind">logo</span>
      </router-link>
    </div>
    <button
      v-if="step === 2 || step === 3"
      type="button"
      class="btn btn__first"
      @click="handleGoToHome"
    >
      cancel
    </button>
    <button
      v-if="step === 2"
      type="button"
      class="btn btn__last"
      @click="handleNext"
    >
      Next
    </button>
    <button
      v-if="step === 3"
      type="button"
      class="btn btn__share"
      @click="handleShare"
    >
      Share
    </button>
  </div>
</template>
<script>
export default {
  name: 'Header',
  props: {
    step: Number
  },
  methods: {
    handleGoToHome () {
      this.$emit('click')
    },
    handleNext () {
      this.$emit('handleNext')
    },
    handleShare () {
      this.$emit('handleShare')
    }
  }
}
</script>
