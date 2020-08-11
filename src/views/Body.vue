<template>
  <div class="body">
    <ul>
      <li
        v-for="item in postList"
        :key="item.id"
      >
        <router-link to="/detail">
          <div class="thumb">
            <img :src="item.image.thumb" :alt="item.title">
          </div>
        </router-link>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: 'Body',
  data () {
    return {
      url: 'http://localhost:3000/memo',
      postList: []
    }
  },
  components: {
  },
  methods: {
    // TODO: write 페이지 만들게되면 submit 예시
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
  },
  mounted () {
    const url = this.url
    this.$http.get(url)
      .then(res => {
        const { data } = res
        this.postList = data
      })
      .catch(err => {
        console.log(err)
      })
  }
}
</script>
