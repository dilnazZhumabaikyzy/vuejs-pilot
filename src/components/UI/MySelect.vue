<template>
    <select :value="modelValue" @change="onChangeOption">
        <option disabled selected="selected" value="">
            Select from above
        </option>
        <option v-for="option in options" :key = "option.value" :value="option.value">
            {{option.name}}
        </option>model
    </select>
</template>
<script>
export default{
    name: 'my-select',
    props: {
        modelValue:{
            type: String
        },
        options: {
            type: Array,
            default: ()=>[]
        }
    },
    methods:{
        onChangeOption(event){
            console.log(event)
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>
<style scoped>

</style>