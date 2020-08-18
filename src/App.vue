<template>
  <div id="app">
    <Header />
    <Body
      :posts="posts"
    />
    <!-- <router-view /> -->
    <Footer />
  </div>
</template>

<script>
import Header from '@/components/Header'
import Footer from '@/components/Footer'
import Body from '@/views/Body'

export default {
  name: 'app',
  data () {
    return {
      posts: []
    }
  },
  components: {
    Header,
    Footer,
    Body
  },
  mounted () {
    this.$http.get(this.$httpUrl)
      .then(res => {
        const { data } = res
        this.posts = data
      })
      .catch(err => console.log(err))
  }
}
</script>

<style lang="scss" src="@/assets/scss/reset.scss"></style>
<style lang="scss" src="@/assets/scss/app.scss"></style>
