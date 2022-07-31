<template>
    <form @submit.prevent>
        <my-input v-model="item.title" type="text" placeholder="Наименование товара"/>
        <textarea v-model="item.description"></textarea>
        <my-input v-model="item.link" type="text" placeholder="Ссылка на изображение"/>
        <my-input v-model="item.price" type="text" placeholder="Цена товара"/>
        <button class="form__button" @click="createItem">Добавить товар</button>
    </form>
</template>

<script>
export default {
    data(){
        return {
            item: {
                title: '',
                description: '',
                link: '',
                price: '',
            }
        }
    },
    methods: {
        createItem(){
            this.item.id = Date.now();
            this.$emit('create', this.item)
            this.item = {
                title: '',
                description: '',
                link: '',
                price: '',
            }
        },
    }
}
</script>

<style lang="scss" scoped>
form{
    max-width: 20.75em;
    padding: 1.5em 1.5em;
}

textarea{
    resize: none;
    width: 100%;
    min-height: 6.75em;
    display: block;
    overflow: hidden;
}

.form__button{
    width: 100%;
}
</style>