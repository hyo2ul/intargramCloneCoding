<template>
  <div class="body">
    <!-- feed -->
    <div
      v-if="step === 1"
      class="post"
    >
      <Post
        v-for="item in posts" :key="item.id"
        :post="item"
        @handleCilck="handleHeart(item)"
      />
    </div>
    <!-- //feed -->
    <!-- phoot upload -->
    <div
      v-if="step === 2"
      class="photo__write"
    >
      <div
        :class="['photo__write--image', selectedFilter]"
        :style="{ 'background-image': 'url('+ image +')' }"
      >
      </div>
      <div class="photo__write--container">
        <!-- where filter choices will be -->
        <FilterType
          v-for="filter in filters"
          :key="filter.name"
          :image="image"
          :filter="filter"
          @click="handleClick"
        />
      </div>
    </div>
    <!-- //phoot upload -->
    <!-- write -->
    <div
      v-if="step === 3"
    >
      <div
        :class="['photo__write--image', selectedFilter]"
        :style="{ 'background-image': 'url('+ image +')' }"
      >
      </div>
      <div class="photo__write--caption">
        <textarea
          :value="value"
          cols="30"
          rows="10"
          placeholder="Write a caption..."
          @keyup="handleKeyup"
        >
        </textarea>
      </div>
    </div>
    <!-- //write -->
  </div>
</template>
<script>
import Post from '@/components/Post'
import FilterType from '@/components/FilterType'

export default {
  name: 'Body',
  props: {
    step: Number,
    image: String,
    selectedFilter: String,
    caption: String,
    posts: Array,
    filters: Array,
    value: String
  },
  components: {
    Post,
    FilterType
  },
  methods: {
    handleHeart (data) {
      const { id } = data
      const url = this.$httpUrl + '/' + id
      const currentPost = this.posts.find(post => post.id)
      currentPost.isHeart ? currentPost.likeCount-- : currentPost.likeCount++
      currentPost.isHeart = !currentPost.isHeart
      this.$http.put(url, data)
        .catch(err => console.log(err))
    },
    handleClick (data) {
      this.$emit('click', data)
    },
    handleKeyup (data) {
      this.$emit('handleKeyup', data)
    }
  },
  mounted () {
  }
}
</script>
