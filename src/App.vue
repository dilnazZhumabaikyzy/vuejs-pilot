<template>
    <div class="app">
        <h3>Posts</h3>
        <my-input v-model="searchQuery"/>
        <div class="app_buttns">
          <my-button @click="showDialogue">Create Post</my-button>
          <my-select v-model="selectedSort" :options = "sortOptions"/>
        </div>
       
        <my-dialogue v-model:show = "dialogueVisible">
          <post-form @create = "createPost"/>
        </my-dialogue>
        <post-list v-if="!isPostsLoading" :posts="sortedAndSearchedPost" @remove = "onDeletePost"/>
        <div v-else><h3>Loading...</h3></div>
        <div class="page-wrapper">
          <div class="pageNumber"
           v-for="pageNumber in totalPages"
           :class="{
            'current-page': page === pageNumber
           }"
           @click="changePage(pageNumber)"
           > {{ pageNumber }}  </div>
        </div>
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
            page: 1,
            limit: 10,
            totalPages: 0,
            selectedSort: '',
            searchQuery: '',
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
        changePage(pageNumber){
          this.page = pageNumber
    
        },
        async fetchPosts(){
          try {
            this.isPostsLoading = true
            
              const response = await axios.get('https://jsonplaceholder.typicode.com/posts',
               {params: {
                  _page: this.page,
                  _limit:this.limit
              }})
              this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
              this.posts = response.data
            
            
          } catch (error) {
            alert('ERROR!')
          } finally{
            this.isPostsLoading = false
          }
        }          
    },
    mounted(){
      this.fetchPosts()
    },
    computed:{
      sortedPost(){
        return [...this.posts].sort((a,b)=> a[this.selectedSort]?.localeCompare(b[this.selectedSort]))
      },
      sortedAndSearchedPost(){
        return this.sortedPost.filter(post=>post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
      }
    },
    watch:{
      page(){
          this.fetchPosts()
      }
    }
}
</script>
<style>
     *{
        margin: 0;
        box-sizing: border-box;
      }
      .app{
        margin: 10px;
      }
      .app_buttns{
        display: flex;
        justify-content: space-between;
        margin: 10px 0;
      }
      .page-wrapper{
        justify-content: center;
        display: flex;
        margin: 5px;

      }
      .pageNumber{
        border: 1px solid teal;
        padding: 3px;
        margin: 2px;
        color: teal;
        font-weight: bold;
      }
      .current-page{
        background-color: teal;
        color: white;
      }

</style>