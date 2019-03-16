<template>
    <div id="single-blog">
        <h1>{{blog.title}}</h1>
        <article>{{blog.content}}</article>
        <p>作者：{{blog.author}}</p>
        <p>分类：</p>
        <ul>
            <li v-for="category in blog.categories" :key="category">
                {{category}}
            </li>
        </ul>
        <router-link class="edit-a" :to="'/edit/' + id">编辑</router-link>
        <button @click="deleteSingleBlog()">删除</button>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: "single-blog",
    data(){
        return{
            id:this.$route.params.id,
            blog:{}
        }
    },
    created(){
        // this.$http.get('https://wd4104105310fmryxd.wilddogio.com/posts/' + this.id + '.json')
        axios.get('/posts/' + this.id + '.json')
            // .then(function(data){
            //     return data.json();
            //     console.log(data)
            // })
            .then((data) =>{
                this.blog = data.data;
            })
    },
    methods:{
        deleteSingleBlog(){
            // this.$http.delete('https://wd4104105310fmryxd.wilddogio.com/posts/' + this.id + '.json')
            axios.delete('https://wd4104105310fmryxd.wilddogio.com/posts/' + this.id + '.json')
                      .then( response =>{
                          this.$router.push({path:'/'})
                      })
        }
    }
}
</script>

<style>
    #single-blog{
        max-width: 960px;
        margin: 0 auto;
        padding: 20px;
        background: #eee;
        border: 1px dotted #aaa;
    }
    .edit-a{
        border: 1px solid #aaa;
        color: #333;
        padding: 2px 5px;
        border-radius: 0;
    }
</style>