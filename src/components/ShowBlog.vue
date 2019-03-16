<template>
  <div v-theme:column="'wide'" id="show-blog">
      <h1>博客总览</h1>
      <input type="text" placeholder="搜索" v-model="search">
      <div v-for="blog in filteredBlogs" class="single-blog">
          <router-link v-bind:to="'/blog/' + blog.id">
            <h2 v-rainbow>{{blog.title | to-uppercase}}</h2>
          </router-link>
          <article>
              {{blog.content | snippet}}
          </article>
      </div>
  </div>
</template>

<script>
export default {
  name: 'show-blog',
  data(){
      return{
          blogs:[],
          search:''
      }
  },
  created(){
      this.$http.get('https://wd4104105310fmryxd.wilddogio.com/posts.json')
      .then(function(data){
        return data.json();
          console.log(data)
        // this.blogs = data.body.slice(0,10);
        // console.log(this.blogs)
      })
      .then(function(data){
        var dataArray = [];
        for(let key in data){
          console.log(key)
          data[key].id = key;
          dataArray.push(data[key])
        }
        this.blogs = dataArray;
        console.log(this.blogs)
      })
  },
  computed:{
    filteredBlogs:function(){
      return this.blogs.filter((blog) => {
        return blog.title.match(this.search);
      })
    }
  },
  filters:{//两种引入写法
    'to-uppercase':function(value){
      return value.toUpperCase();
    },
    snippet(value){
      return value.slice(0,100) + '...';
    }
  },
  directives:{
    rainbow:{
      bind:function(el,binding,vnode){
        el.style.color = '#' + Math.random().toString(16).slice(2,8);
      }
    }
  }
}
</script>

<style scope>
#show-blogs{
    max-width: 800px;
    margin: 0 auto;
}
.single-blog{
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
}

#show-blog a{
  color: #444;
  text-decoration: none;
}
input[type="text"]{
  padding: 8px;
  width: 100%;
  box-sizing: border-box;
}
</style>
