<template>
    <select v-model="modelValue" @change="changeOption" class="select">
        <option disabled value="" >По умолчанию</option>
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
    position: relative;
    appearance: none;
    font-family: 'SourceSansPro', 'Arial', sans-serif;
    font-size: 0.75em;
    line-height: 1.25em;
    width: 10em;
    height: 3em;
    padding-left: 1.25em;
    color: #B4B4B4;
    outline: none;
    border: none;
    border-radius: 0.33em;
    background-color: #FFFEFB;
    box-shadow: 0em 0.16em 0.41em rgba(0, 0, 0, 0.1);
    background-image: url("/public/img/select.svg");
    background-repeat: no-repeat;
    background-position-y: 50%;
    background-position-x: 85%;
}
</style>