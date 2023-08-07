<template>
    <form @submit.prevent>
            <h4>Form</h4>
            <input v-model="post.title" class="input"  type="text" >
            <input  class="input" type="text" v-model="post.body">
            <button class="button" @click="createPost">Go</button>
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
      .input{
        border: 1px solid teal;
        margin: 5px;
        padding: 10px 15px;
      }
      .button {
        margin: 5px;
        padding: 5px;
      }
</style>