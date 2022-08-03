<template>
    <form @submit.prevent>
        <div class="input-wrapper">
            <div class="input__title req">Наименование товара</div>
            <my-input v-model="item.title" type="text" placeholder="Введите наименование" :class="{error: !titleIsValid}"/>
            <div v-if="!titleIsValid" class="hint">Поле является обязательным и должно содержать только буквы</div> 
        </div>
        <div class="input__title">Описание товара</div>
        <textarea v-model="item.description"></textarea>
        <div class="input-wrapper">
            <div class="input__title req">Ссылка на изображение товара</div>
            <my-input v-model="item.link" type="text" placeholder="Введите ссылку" :class="{error: !linkIsValid}"/>
            <div v-if="!linkIsValid" class="hint">Поле является обязательным(более 1 символа.домен)без!$^*;'"` </div>
        </div>
        <div class="input-wrapper">
            <div class="input__title req">Цена товара</div>
            <my-input v-model="item.price" type="text" placeholder="Введите цену" :class="{error: !priceIsValid}"/>
            <div v-if="!priceIsValid" class="hint">Поле является обязательным и должно содержать только цифры </div>
        </div>
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
            return /^[а-яёa-z\s]+$/i.test(this.item.title);
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
    height: fit-content;
    padding: 1.5em;
    border-radius: 0.25em;
}

textarea{
    resize: none;
    outline: none;
    line-height: 1.25em;
    width: 100%;
    min-height: 9em;
    margin-bottom: 1.33em;
    display: block;
    overflow: auto;
    padding: 0.83em 1.33em 0;
    border: none;
    border-radius: 0.33em;
    box-shadow: 0em 0.16em 0.41em rgb(0 0 0 / 10%);
}

.form__button{
    text-align: center;
    font-family: 'Inter', sans-serif;
    font-size: 0.75em;
    min-height: 3em;
    line-height: 1.25em;
    margin-top: 0.33em;
    border: none;
    border-radius: 0.83em;
    background-color: #7BAE73;
    color: #FFFFFF;
    box-shadow: 0px 0.16em 0.33em rgba(0, 0, 0, 0.1);
    cursor: pointer;
    transition: 500ms;
}

.form__button:disabled{
    background-color: #EEEEEE;;
    color: #B4B4B4;
    box-shadow: none;
}

.error{
    border: 0.08em solid #FF8484;
    color:#FF8484;
}

.hint{
    position: absolute;
    font-size: 0.6em;
    color: #FF8484;
    margin-top: 0.38em;
}

.input-wrapper{
    margin-bottom: 1.2em;
    position: relative;
}
.input__title{
    display: flex;
    font-size: 0.7em;
    margin-bottom: 0.36em;
    line-height: 1.3em;
}

.input__title.req::after{
    content: '';
    flex: 0 0 0.4em;
    height: 0.4em;
    background-color: #FF8484;
    border-radius: 50%;
    transform: translateX(0.2em);
}
</style>