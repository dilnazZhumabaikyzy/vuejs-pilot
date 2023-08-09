<template>
    <input type="text" class="input" :value="modelValue" @input="updateInput">
</template>
<script>
export default{
    name: 'my-input',
    props:{
        modelValue: [String, Number]
    },
    methods: {
        updateInput(event){
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>
<style scoped>
      .input{
        border: 1px solid teal;
        margin: 5px;
        padding: 10px 15px;
        width: 100%;
      } 
</style>