<template>
  <div class="post__item">
    <div class="users">
      <div class="users__profile">
        <img :src="post.profile" :alt="post.userName" />
      </div>
      <a href="#" class="users__name">{{ post.userName }}</a>
    </div>
    <div class="thumb">
      <img :src="`/img/${post.image}`" :alt="post.title" />
    </div>
    <div class="likes">
      <button
        typee="button"
        class="btn btn-sm likes__button"
        @click="handleHeart(post)"
      >
        <b-icon :icon="post.isHeart ? 'heart-fill' : 'heart'"></b-icon>
      </button>
      <span class="count">{{ post.likeCount }} likes</span>
    </div>
    <p class="caption">
      <span class="caption__name">{{ post.userName }}</span>
      {{ post.caption }}
    </p>
  </div>
</template>
<script>
export default {
  name: 'Post',
  props: {
    post: Object
  },
  methods: {
    handleHeart (data) {
      this.$emit('handleCilck', data)
    }
  }
}
</script>
