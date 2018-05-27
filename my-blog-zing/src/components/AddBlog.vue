<template>
  <div class="add-blog">
    <h2>添加博客</h2>
    <form v-if="!submmited">
      <label>博客标题</label>
      <input type="text" v-model="blog.title" required/>

      <label>博客内容</label>
      <textarea v-model="blog.content"></textarea>

      <div id="checkboxes">
        <label>Vue.js</label>
        <input type="checkbox" value="Vue.js" v-model="blog.categories"/>
        <label>Node.js</label>
        <input type="checkbox" value="Node.js" v-model="blog.categories"/>
        <label>React.js</label>
        <input type="checkbox" value="React.js" v-model="blog.categories"/>
        <label>Angular4.js</label>
        <input type="checkbox" value="Angular4.js" v-model="blog.categories"/>
      </div>
      <label>作者：</label>
      <select v-model="blog.author">
        <option v-for="author in authors">
          {{author}}
        </option>
      </select>
      <!--v-on:click.prevent:关键字prevent阻止刷新页面-->
      <button v-on:click.prevent="post">添加博客</button>
    </form>
    <div v-if="submmited">
      <h3>你的博客发布成功！</h3>
    </div>

    <div id="preview">
      <h3>博客总览</h3>
      <p>博客标题：{{blog.title}}</p>
      <p>博客内容：</p>
      <p>{{blog.content}}</p>
      <p>博客分类：</p>
      <ul>
        <li v-for="category in blog.categories">
          {{category}}
        </li>
      </ul>
      <p>作者：{{blog.author}}</p>
    </div>
  </div>
</template>

<script>
  export default {
    //http://jsonplaceholder.typicode.com/
    //http://jsonplaceholder.typicode.com/posts
    name: 'add-blog',
    data () {
      return {
        blog:{
          title:"",
          content:"",
          categories:[],
          author:""
        },
        authors:["路明非","芬格尔","陈墨瞳","凯撒.加图索","楚子航"],
        submmited:false
      }
    },
    methods:{
      post:function(){
        this.$http.post("http://jsonplaceholder.typicode.com/posts",{
          title:this.blog.title,
          body:this.blog.content,
          userId:1
        })
          .then(function (data) {
            console.log(data);
            this.submmited = true;
          })
  }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
