<template>
    <div>
        <h3>List of Posts</h3>
        <post-item v-for="post in posts" :post = "post" />
    </div>
</template>
<script>
import PostItem from './PostItem.vue';
export default {
    components: 
    {PostItem},
    props:{
        posts: {
            type: Array,
            required: true
        }
    }
}
</script>
<style scoped>
 .post{
        padding: 15px;
        border: solid green 2px;
        margin: 3px;
      }
</style>