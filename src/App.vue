<template>
    <div class="app">
        <post-form @create = "createPost"/>
        <post-list v-bind:posts="posts"/>
    </div>
</template>
<script>
import PostForm from './components/PostForm';
import PostList from './components/PostList';
export default{
      components:{
        PostForm, PostList
      },
    data(){
        return{
            posts: [ 
            { id: '1', title: 'js', body: 'Description 1'},
            { id: '2', title: 'java', body: 'Description 3'},
            { id: '3', title: 'php', body: 'Description 4'},
            { id: '4', title: 'go', body: 'Description 5'},
        ]
        }
    },
    methods: {
        createPost(post){
          // console.log(post)
          this.posts.push(post)
        }
          
    }
}
</script>
<style>
     *{
        margin: 0;
      }
      .app{
        margin: 10px;
      }

</style>