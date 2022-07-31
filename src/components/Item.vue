<template>
    <div class="item">
        <div class="image__container"></div>
        <div class="wrapper">
            <div class="title">{{item.title}}</div>
            <div class="description">{{item.description}}</div>
            <div class="price">{{item.price}}</div>
        </div>
        <button @click="$emit('remove', item)" class="item__button">Удалить</button>
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
    background-color: azure;
    width: 20.75em;
}
</style>