<template>
  <div id="app">
    <!-- <add-blog></add-blog> -->
    <!-- <show-blog></show-blog> -->
    <blog-header></blog-header>
    <router-view></router-view>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld'

import AddBlog from './components/AddBlog'
import ShowBlog from './components/ShowBlog'
import BlogHeader from './components/BlogHeader'

export default {
  name: 'App',
  components: {
    AddBlog,ShowBlog,BlogHeader
  }
}
</script>

<style>
/* #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
