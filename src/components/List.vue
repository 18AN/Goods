<template>
    <div>
        <div class="list" >
            <transition-group name="list-item">
                <Item v-for="item in items" :item="item" :key="item.id" @remove="$emit('remove', item)"/>
            </transition-group>
        </div> 
    </div>
</template>

<script>
import Item from './Item.vue'
export default {
  components: { Item },
    props: {
        items: {
            type: Array,
            reqired: true
        }
    }
}
</script>

<style lang="scss" scoped>
.list{
    max-width: 64.25em;
    display: flex;
    flex-wrap: wrap;
    background-color: bisque;
    gap: 1em;
}

.list-item {
  display: inline-block;
  margin-right: 10px;
}
.list-item-enter-active,
.list-item-leave-active {
  transition: all 0.3s ease;
}
.list-item-enter-from,
.list-item-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
.list-item-move {
  transition: transform 0.4s ease;
}
</style>