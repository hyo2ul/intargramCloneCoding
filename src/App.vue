<template>
  <div id="app">
    <Header
      :step="step"
      @click="handleGoToHome"
      @handleNext="handleNext"
      @handleShare="handleShare"
    />
    <Body
      v-model="caption"
      :step="step"
      :posts="posts"
      :selectedFilter="selectedFilter"
      :filters="filters"
      :image="image"
      @click="handleClick"
      @handleKeyup="handleKeyup"
    />
    <Footer
      ref="footer"
      :step="step"
      @handleChange="uploadImage"
      @click="handleGoToHome"
    />
  </div>
</template>

<script>
import Header from '@/components/Header'
import Footer from '@/components/Footer'
import Body from '@/views/Body'
import filters from '@/data/filter'

export default {
  name: 'app',
  data () {
    return {
      step: 1,
      image: '',
      caption: '',
      selectedFilter: '',
      posts: [],
      filters
    }
  },
  components: {
    Header,
    Footer,
    Body
  },
  methods: {
    uploadImage (evt) {
      const files = evt.target.files
      const inputFile = this.$refs.footer.$refs.inputFile
      if (!files.length) return
      const reader = new FileReader()
      reader.readAsDataURL(files[0])
      reader.onload = evt => {
        this.image = evt.target.result
        this.step = 2
      }
      inputFile.value = ''
    },
    handleClick ({ name }) {
      this.selectedFilter = name
    },
    handleGoToHome () {
      this.image = ''
      this.selectedFilter = ''
      this.caption = ''
      this.step = 1
    },
    handleNext () {
      this.step++
    },
    handleShare () {
      const param = {
        id: this.posts.length + 1,
        image: this.image,
        filter: this.selectedFilter,
        profile: 'https://picsum.photos/id/233/200/300',
        userName: 'userName',
        likeCount: 0,
        isHeart: false,
        hashtag: '#먹스타그램',
        caption: this.caption
      }
      console.log(param)
      const url = this.$httpUrl
      this.$http.post(url, param)
        .then(res => {
          this.handleGoToHome()
          this.getPosts()
        })
        .catch(err => console.log(err))
    },
    handleKeyup ({ target }) {
      this.caption = target.value
    },
    getPosts () {
      this.$http.get(this.$httpUrl)
        .then(res => {
          const { data } = res
          data.sort((a, b) => {
            return b.id - a.id
          })
          this.posts = data
        })
        .catch(err => console.log(err))
    }
  },
  mounted () {
    this.getPosts()
  }
}
</script>

<style lang="scss" src="@/assets/scss/reset.scss"></style>
<style lang="scss" src="@/assets/scss/app.scss"></style>
