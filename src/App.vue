<template>
    <div class="container">
        <div class="header">
            <div class="header__title">Добавление товара</div>
            <my-select v-model="selectedSort" :options="sortOptions"/>
        </div>
        <div class="main">
            <Form  @create="createItem" class="form-component"/>
            <List :items="sortedItems" @remove="removeItem" class="list-componenet" />
        </div>
    </div>
    
</template>

<script>
import Form from '@/components/Form.vue';
import List from '@/components/List.vue';
export default {
    components: {
        Form, List
    },
    data() {
        return {
            items: [],
            staticItems: [
                {id: 1, title: 'A', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link: '/img/item.svg', price: '10000'},
                {id: 2, title: 'B', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link: '/img/item.svg', price: '20000'},
                {id: 3, title: 'C', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link: '/img/item.svg', price: '30000'},
                {id: 4, title: 'D', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link: '/img/item.svg', price: '40000'},
                {id: 5, title: 'E', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link: '/img/item.svg', price: '50000'},
                {id: 6, title: 'F', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link: '/img/item.svg', price: '60000'},
                {id: 7, title: 'G', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link: '/img/item.svg', price: '70000'},
                {id: 8, title: 'H', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link: '/img/item.svg', price: '80000'},
                {id: 9, title: 'I', description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', link: '/img/item.svg', price: '90000'},
            ],
            selectedSort: '',
            sortOptions: [
                {value: 'title', name: 'По наименованию'},
                {value: 'priceUp', name: 'По возрастанию цены'},
                {value: 'priceDown', name: 'По убыванию цены'},
            ]
        }
    },
    mounted() {
        if (!localStorage.getItem('items')) { 
            localStorage.setItem('items',JSON.stringify(this.staticItems));
            this.items = JSON.parse(localStorage.getItem('items'));
        }else{
            this.items = JSON.parse(localStorage.getItem('items'));
        }
    },
    methods: {
        createItem(item){
            this.items.push(item);
            this.saveItems();
        },
        removeItem(item){
            this.items = this.items.filter(i => i.id !== item.id);
            this.saveItems();
        },
        saveItems() {
            const parsed = JSON.stringify(this.items);
            localStorage.setItem('items', parsed);
        },
    },
    computed: {
        sortedItems(){
            return [...this.items].sort((item1, item2) => {
                if(this.selectedSort === 'title'){
                    return item1.title?.localeCompare(item2.title)
                }else if(this.selectedSort === 'priceUp'){
                    return item1.price - item2.price
                }else if(this.selectedSort === 'priceDown'){
                                        if(Number(item1.price) > Number(item2.price)){
                        return -1
                    }else if(Number(item1.price) < Number(item2.price)){
                        return 1
                    }else if(Number(item1.price) === Number(item2.price)){
                        return 0
                    }
                }
            })
        }
    },
}
</script>

<style lang="scss">
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
html{
    font-family: 'SourceSansPro', 'Arial', sans-serif;
    color: #3F3F3F;
}

body{
    background-color: rgba(255, 254, 251, 0.8);
    padding-bottom: 2em;
}

.container{
    max-width: 86em;
    margin: 2em auto 0;
    background-color: rgba(255, 254, 251, 0.8);
}
.main{
    display: flex;
    gap: 1em;
}
.form-component{
    background-color: #FFFEFB;
    box-shadow: 0px 1.25em 1.87em rgba(0, 0, 0, 0.04), 0px 0.37em 0.62em rgba(0, 0, 0, 0.02);
    position: sticky;
    top: 1.5em;
}

.header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1em;
    &__title{
        font-size: 1.75em;
        font-weight: 600;
        line-height: 1.25em;
        color: #3F3F3F;
    }
}

button{
    width: 100%;
}

@media(max-width: 1024px){
    .container{
        margin-top: 3em;
    }
    .form-component{
        background-color: transparent;
        box-shadow: none;
        position: fixed;
        top: -25.5em;
        z-index: 1;
        transition: 500ms;
        & > .form__button{
            transform: translateY(1.6em);
        }
    }
    .form-component:hover{
        top: 0em;
        background-color:  #FFFEFB;
        transition: 500ms;
        & > .form__button{
            transform: translateY(0em);
        }
    }
    .list{
        justify-content: center;
    }
    .header{
        justify-content: center;
        gap: 1em;
    }
    .main{
        justify-content: center;
    }
}
@media(max-width: 480px){
    .header{
        gap: 0em;
        &__title{
            display: none;
        }
    }
}

</style>