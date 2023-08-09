<template>
    <div class="app">
        <h3>Posts</h3>
        <my-button @click="showDialogue">Create Post</my-button>
        <my-dialogue v-model:show = "dialogueVisible">
          <post-form @create = "createPost"/>
        </my-dialogue>
        <post-list v-bind:posts="posts" @remove = "onDeletePost"/>
    </div>
</template>
<script>
import PostForm from './components/PostForm';
import PostList from './components/PostList';
import MyButton from './components/UI/MyButton.vue';
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
        ],
        dialogueVisible: false
        }
    },
    methods: {
        createPost(post){
          // console.log(post)
          this.posts.push(post)
        },
        onDeletePost(post){
          this.posts = this.posts.filter(p=> p.id != post.id)
        },
        showDialogue(){
          this.dialogueVisible = true
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