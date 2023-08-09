<template>
    <div class="app">
        <h3>Posts</h3>
        <div class="app_buttns">
          <my-button @click="showDialogue">Create Post</my-button>
          <my-select v-model="selectedSort" :options = "sortOptions"/>
        </div>
        <my-button @click = "fetchPosts">Get Posts</my-button>
        <my-dialogue v-model:show = "dialogueVisible">
          <post-form @create = "createPost"/>
        </my-dialogue>
        <post-list v-if="!isPostsLoading" v-bind:posts="posts" @remove = "onDeletePost"/>
        <div v-else><h3>Loading...</h3></div>
    </div>
</template>
<script>
import PostForm from './components/PostForm';
import PostList from './components/PostList';
import MyButton from './components/UI/MyButton.vue';
import axios from 'axios'
export default{
    components:{
      PostForm, PostList
    },
    data(){
        return{
            posts: [],
            dialogueVisible: false,
            isPostsLoading: false,
            selectedSort: '',
            sortOptions: [
              {value: 'title', name: 'by Title'},
              {value: 'body', name: 'by Body'}
        ]
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
        },
        async fetchPosts(){
          try {
            this.isPostsLoading = true
            setTimeout(async () => {
              const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
              this.posts = response.data
              this.isPostsLoading = false
            }, 1000)
            // const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
            // this.posts = response.data
          } catch (error) {
            alert('ERROR!')
          }
        }          
    },
    mounted(){
      this.fetchPosts()
    },
    watch:{
      selectedSort(newValue){
        this.posts.sort((a,b)=>{
          return a[newValue]?.localeCompare(b[newValue])
        })
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
      .app_buttns{
        display: flex;
        justify-content: space-between;
        margin: 10px 0;
      }

</style>