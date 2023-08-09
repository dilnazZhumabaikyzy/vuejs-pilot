<template>
    <div class="post">
        <div>
            <div><strong>Title: </strong> {{ post.title }}</div>
            <div><strong>Description: </strong> {{ post.body }}</div>
        </div>
        <div class="post_buttons">
            <my-button @click = "$emit('remove', post)">Delete</my-button>
        </div>
    </div>
</template>
<script>
import MyButton from '@/components/UI/MyButton'
export default{
    components:{
        MyButton
    },
    props: {
        post:{
            type: Object,
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
        display: flex;
        align-items: center;
        justify-content: space-between;
      }
</style>