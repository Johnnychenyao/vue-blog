<template>
  <div id="add-blog">
    <h2>编辑博客</h2>
    <form v-if="!submitted">
      <label>博客标题</label>
      <input type="text" v-model="blog.title" required>

      <label>博客内容</label>
      <textarea v-model="blog.content"></textarea>

      <div id="checkboxes">
        <label>Vue.js</label>
        <input type="checkbox" value="vue.js" v-model="blog.categories">
        <label>Node.js</label>
        <input type="checkbox" value="Node.js" v-model="blog.categories">
        <label>React.js</label>
        <input type="checkbox" value="React.js" v-model="blog.categories">
        <label>Angular.js</label>
        <input type="checkbox" value="Angular.js" v-model="blog.categories">
      </div>
      <label>作者：</label>
      <select v-model="blog.author">
        <option v-for="author in authors" :key="author">
          {{author}}
        </option>
      </select>
      <button @click.prevent="post">编辑博客</button>
    </form>

    <div v-if="submitted">
      <h3>您的博客发布成功</h3>
    </div>

    <div id="preview">
      <h3>博客总览</h3>
      <p>博客标题：{{blog.title}}</p>
      <p>博客内容：</p>
      <p>{{blog.content}}</p>
      <p>博客分类：</p>
      <ul>
        <li v-for="category in blog.categories" :key="category">
          {{category}}
        </li>
      </ul>
      <p>作者：{{blog.author}}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  //http://jsonplaceholder.typicode.com/
  name: 'add-blog',
  data () {
    return {
      id:this.$route.params.id,
      blog:{},
      authors:["Hemiah","Henry","Bucky"],
      submitted:false
    }
  },
  methods:{
    fetchData(){
      // this.$http.get("https://wd4104105310fmryxd.wilddogio.com/posts/" + this.id + ".json")
      axios.get("/posts/" + this.id + ".json")
            // .then(function(data){
                // return data.json();
                // console.log(data)
                // this.blog = data.body;
            // })
            .then((data) =>{
                this.blog = data.data;
            })
    },
    post:function(){
      // this.$http.put("https://wd4104105310fmryxd.wilddogio.com/posts/" + this.id + ".json",this.blog)
      axios.put("/posts/" + this.id + ".json",this.blog)
                .then((data) =>{
                  console.log(data)
                  this.submitted = true;
                })
    }
  },
  created(){
      this.fetchData();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#app-blog *{
  box-sizing: border-box;
}
#add-blog{
  margin: 20px auto;
  max-width: 600px;
  padding: 20px;
}
label{
  display: block;
  margin: 20px 0 10px;
}
input[type="text"],textarea,select{
  display: block;
  width: 100%;
  padding: 8px;
}
textarea{
  height: 200px;
}
#checkboxes label{
  display: inline-block;
  margin-top: 0;
}
#checkboxes input{
  display: inline-block;
  margin-right: 10px;
}
button{
  display: block;
  margin: 20px 0;
  background: crimson;
  color: #fff;
  border: 0;
  padding: 14px;
  border-radius: 4px;
  font-size: 18px;
  cursor: pointer;
}
#preview{
  padding: 10px 20px;
  border:1px dotted #ccc;
  margin: 30px 0;
}
h3{
  margin-top: 10px;
}
</style>
