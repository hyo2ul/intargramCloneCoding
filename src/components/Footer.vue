<template>
  <div class="footer">
    <div class="footer__inner">
      <button
        @click="handleGoToHome"
        type="button"
        class="footer__inner--home"
      >
        <b-icon icon="house-fill"></b-icon>
      </button>
      <span class="footer__inner--file">
        <input
          ref="inputFile"
          :disabled="step !== 1"
          type="file"
          id="file"
          class="inputFile"
          @change="uploadImage"
        />
        <label for="file">
          <b-icon icon="plus-square"></b-icon>
        </label>
      </span>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Footer',
  props: {
    step: Number
  },
  methods: {
    uploadImage (evt) {
      this.$emit('handleChange', evt)
    },
    handleGoToHome () {
      this.$emit('click')
    }
  }
}
</script>
