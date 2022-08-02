<template>
    <select v-model="modelValue" @change="changeOption" class="select">
        <option disabled value="" >Сортировать по</option>
        <option v-for="option in options" :key="option.value" :value="option.value">{{option.name}}</option>
    </select>
</template>

<script>
export default {
    name: 'my-select',
    props: {
        modelValue: {
            type: String,

        },
        options: {
            type: Array,
            default: () => []
        }
    },
    methods: {
        changeOption(event){
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>

<style lang='scss' scoped>
.select{
    font-family: 'SourceSansPro', 'Arial', sans-serif;
    font-size: 0.75em;
    width: 12em;
    height: 3em;
    color: #B4B4B4;
    outline: none;
    border: none;
    border-radius: 0.33em;
    background-color: #FFFEFB;
    box-shadow: 0em 0.16em 0.41em rgba(0, 0, 0, 0.1);
}
</style>