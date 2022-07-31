<template>
    <div class="container">
        <div class="header">
            <h1>Добавление товара</h1>
            <my-select v-model="selectedSort" :options="sortOptions"/>
        </div>
        <div>
            <Form  @create="createItem"/>
            <List :items="sortedItems" @remove="removeItem"/>
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
                {id: 1, title: 'A', description: 'Описание товара', price: '1'},
                {id: 2, title: 'B', description: 'Описание товара', price: '2'},
                {id: 3, title: 'C', description: 'Описание товара', price: '3'},
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

body{
    background-color: #E5E5E5;
}

.container{
    max-width: 86em;
    margin: 2em auto 0;
    background-color: rgba(255, 254, 251, 0.8);;
}

.header{
    display: flex;
    justify-content: space-between;
    align-items: center;
}

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
input{
    width: 100%;
}

button{
    width: 100%;
}
</style>