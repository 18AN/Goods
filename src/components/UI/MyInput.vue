<template>
    <input :value="modelValue" @input="updateInput" type="text">
</template>

<script>
export default {
    name: 'my-input',
    props: {
        modelValue: [String, Number],
    },
    methods: {
        updateInput(event){
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>

<style lang='scss' scoped>
    input{
    min-width: 23.66em;
    outline: none;
    font-family: 'SourceSansPro', 'Arial', sans-serif;;
    font-size: 0.75em;
    line-height: 1.25em;
    min-height: 3em;
    padding-left: 1.33em;
    border: none;
    border-radius: 0.33em;
    box-shadow: 0em 0.16em 0.41em rgb(0 0 0 / 10%);
}
</style>