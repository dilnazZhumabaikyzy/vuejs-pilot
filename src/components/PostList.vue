<template>
    <div v-if="posts.length > 0">
        <h3>List of Posts</h3>
        <transition-group name="post-list">
            <post-item 
            v-for="post in posts" 
            :post = "post"
            :key="post.id"
            @remove ="$emit('remove', post)"
            />
        </transition-group>
    </div>
    <h3 v-else style="color: teal">No posts yet</h3>
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
 .post-list-enter-active,
.post-list-leave-active {
  transition: all 0.3s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}
.post-list-move{
    transition: transform 0.5s ease;
}
</style>