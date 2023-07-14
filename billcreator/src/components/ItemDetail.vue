<template>
<div class="item-card">
    <h4 class="item-title">{{ title }}</h4>
    <p class="item-description"><strong>Descripcion: </strong>{{ description }}</p>
    <div class="item-price">
        <strong class="highlighted">Precio: </strong>
        <span>
            $ {{ price }}
        </span>
    </div>
    <div class="item-discount" v-if="discount">
        <i class="highlighted">Descuento:</i>
        <br>{{ discountValue }} %
    </div>
    <div v-else>
        <i class="highlighted">Descuento:</i>
        No disponible
    </div>
    <button 
    class="add-item"
    @click="handleClick">
    Agregar item
    </button>
</div>

</template>

<script lang="ts" setup>

export interface Item {
  title : string,
  description : string,
  price : number,
  discount : boolean,
  discountValue : number,
}

const props = defineProps<{
    title : string
    description : string
    price : number
    discount : boolean
    discountValue : number 
}>();

let item: Item = {
    title : props.title,
    description : props.description,
    price : props.price,
    discount : props.discount,
    discountValue : props.discountValue
}

const emit = defineEmits<{
    (event : 'selectItem', item : Item):void
}>();

const handleClick = () => {
    emit('selectItem', item)
}

</script>

<style scoped>
.item-card {
    display: grid;
    grid-template-rows: 10% 50% 10% 20% 10%;
    padding: 3px;
    padding-bottom: 1px;
    border: 3px solid black;
}

.item-title {
    margin-top: 0;
    padding-top: 2px;
    text-align: center;
    text-decoration: underline;
}

.item-description {
    margin: 0;
    margin-top: 3px;
    padding-top: 10px;
    overflow-x: hidden;
}

.item-price {
    align-content: center;
    padding-top: 3px;
}

.item-discount {
    margin: 0;
}

.highlighted {
    text-decoration: underline;
}

.add-item {
    width: 90%;
    margin: 0 auto;
}
</style>