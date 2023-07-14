<template>
<li>
    <button @click="handleClick">X</button>
    {{ props.title }}
    <span class="item-unit-price">{{ props.price }}</span>
</li>
</template>

<script lang="ts" setup>

const props = defineProps<{
    title : string
    price : number
}>();

const emit = defineEmits<{
    (event : 'deleteItem'): void
}>();

const handleClick = ()=>{
    emit('deleteItem');
}

</script>

<style scoped>
.item-unit-price {
    width: 15px;
    text-align: center;
}
</style>