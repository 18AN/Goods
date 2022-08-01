<template>
    <form @submit.prevent>
        <my-input v-model="item.title" type="text" placeholder="Наименование товара"/>
        <p v-if="!titleIsValid">Поле является обязательным и должно содержать только буквы</p>
        <textarea v-model="item.description"></textarea>
        <my-input v-model="item.link" type="text" placeholder="Ссылка на изображение"/>
        <p v-if="!linkIsValid">Поле является обязательным(более 1 символа.домен)без!$^*;'"` </p>
        <my-input v-model="item.price" type="text" placeholder="Цена товара"/>
        <p v-if="!priceIsValid">Поле является обязательным и должно содержать только цифры </p>
        <button class="form__button" :disabled="!formIsValid" @click="createItem">Добавить товар</button>
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
    computed: {
        titleIsValid(){
            return /^[а-яёa-z]+$/i.test(this.item.title);
        },
        linkIsValid(){
            return /[-a-zA-Z0-9@:%_\+.~#?&\/=]{2,256}\.[a-z]{2,4}\b(\/[-a-zA-Z0-9@:%_\+.~#?&\/=]*)?/gi.test(this.item.link);
        },
        priceIsValid(){
            return /^\d+$/.test(this.item.price);
        },
        formIsValid(){
            return this.titleIsValid && this.linkIsValid && this.priceIsValid;
        },
    },
    methods: {
        createItem(){
            if(this.formIsValid){
                this.item.id = Date.now();
                this.$emit('create', this.item)
                this.item = {
                    title: '',
                    description: '',
                    link: '',
                    price: '',
                }
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