<template>
  <div class="body">
    <div class="post">
      <Post
        v-for="item in posts" :key="item.id"
        :post="item"
        @handleCilck="handleHeart(item)"
      />
    </div>
  </div>
</template>
<script>
import Post from '@/components/Post'

export default {
  name: 'Body',
  props: {
    posts: Array
  },
  components: {
    Post
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
    }
    // TODO: write 페이지 만`들게되면 submit 예시
    // handleSubmit (data) {
    //   const id = this.postList.length + 1
    //   const newData = Object.assign({
    //     ...data,
    //     id
    //   })
    //   const url = this.url
    //   const param = newData
    //   this.$http.post(url, param)
    //     .then(res => {
    //       const { data } = res
    //       console.log(data)
    //     })
    //     .catch(err => {
    //       console.log(err)
    //     })
    // }
  }
}
</script>
