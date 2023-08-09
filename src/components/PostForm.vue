<template>
    <form @submit.prevent>
            <h4>Form</h4>
            <my-input v-model="post.title"/>
            <my-input v-model="post.body"/>
            <my-button @click="createPost" style=" margin-top: 15px;">Go</my-button>
    </form>
</template>
<script>
export default{  
    data(){
        return{
            post: {
                title: '',
                body: ''
            }
        }
    },
    methods:{
        createPost(){
          this.post.id = Date.now()
         
          this.$emit('create', this.post)
          this.post = {
                title: '',
                body: ''
            }         
        }
    }
}
</script>
<style scoped>
 form{
        display: flex;
        flex-direction: column;
      }
    
</style>