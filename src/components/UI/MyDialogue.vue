<template>
<div class="dialogue" v-if="show" @click.stop="hideDialogue">
    <div @click.stop class="dialogue-content">
        <slot></slot>
    </div>
</div>
</template>
<script>
export default{
     name: 'my-dialogue',
     props: {
        show: {
            type: Boolean,
            default: false
        }
     },
     methods:{
        hideDialogue(){
            this.$emit('update:show', false)
        }
     }
}
</script>
<style scoped>
.dialogue{
    background: rgba(0, 0, 0, 0.5);
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    position: fixed;
}
.dialogue-content{
    background: white;
    padding: 20px;
    margin: auto;
    min-height: 50px;
    min-width: 300px;
    border-radius: 12px;
}
</style>