<template>
    <div class="item">
        <div class="image__container">
            <img :src="item.link" alt="Изображение товара">
        </div>
        <div class="wrapper">
            <div class="title">{{item.title}}</div>
            <div class="description">{{item.description}}</div>
            <div class="price">{{item.price}}</div>
        </div>
        <button @click="$emit('remove', item)" class="item__button"><img src="/img/delete.svg" alt=""></button>
    </div>
</template>

<script>
export default {
    props: {
        item: {
            type: Object,
            required: true
        }
    }
}
</script>

<style lang="scss" scoped>
.item{
    position: relative;
    background-color: #FFFEFB;
    border: none;
    border-radius: 0.25em;
    width: 20.75em;
    box-shadow: 0em 1.25em 0.87em rgba(0, 0, 0, 0.04), 0em 0.37em 0.62em rgba(0, 0, 0, 0.02);
}
.title{
    font-size: 1.25em;
    font-weight: 600;
    line-height: 1.25em;
}
.price{
    font-size: 1.5em;
    font-weight: 600;
    line-height: 1.25em;
}
.item__button{
    display: none;
    background-color: #FF8484;
    font-size: inherit;
    border: none;
    width: 2em;
    height: 2em;
    position: absolute;
    top: -0.5em;
    right: -0.5em;
    border-radius: 0.62em;
}

.item:hover > .item__button{
    display: block;
}
.image__container{
    height: 12.5em;
    overflow: hidden;
}
.wrapper{
    padding: 1em 1em 1.5em;
}
.description{
    height: 5em;
    overflow: auto;
    line-height: 1.25em;
    margin-bottom: 2em;
}

</style>