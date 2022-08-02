<template>
    <div class="container">
        <div class="header">
            <div class="header__title">Добавление товара</div>
            <my-select v-model="selectedSort" :options="sortOptions" class="select"/>
        </div>
        <div class="main">
            <Form  @create="createItem" class="form-component"/>
            <List :items="sortedItems" @remove="removeItem" class="list-component"/>
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
            items: [
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
    methods: {
        createItem(item){
            this.items.push(item);
        },
        removeItem(item){
            this.items = this.items.filter(i => i.id !== item.id)
        }
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
    font-family: 'SourceSansPro', 'Arial', sans-serif;;
}
img{
    max-width: 100%;
}

body{
    background-color: rgba(255, 254, 251, 0.8);
}

.container{
    max-width: 86em;
    margin: 3em auto 0;
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
    margin-bottom: 1.5em;
    &__title{
        font-size: 1.75em;
        font-weight: 600;
        line-height: 2.18em;
    }
}
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

button{
    width: 100%;
}

@media(max-width: 1024px){
    .form-component{
        background-color: transparent;
        box-shadow: none;
        position: fixed;
        top: -29em;
        z-index: 1;
        transition: 500ms
    }
    .form-component:hover{
        top: 0em;
        background-color:  #FFFEFB;
        transition: 500ms
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