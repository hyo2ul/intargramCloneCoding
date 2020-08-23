<template>
  <div class="filter__item">
    <strong class="filter__item--name">{{ filter.name }}</strong>
    <div
      :class="filter.name"
      :style="{ 'background-image': 'url('+ image +')' }"
      @click="handleClick(filter)"
    >
    </div>
  </div>
</template>
<script>

export default {
  name: 'FileType',
  props: {
    filter: Object,
    image: String
  },
  methods: {
    handleClick (data) {
      this.$emit('click', data)
    }
  }
}
</script>
<style lang="scss" src="@/assets/scss/filter.scss"></style>
