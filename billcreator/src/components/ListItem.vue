<template >
  <ItemDetail v-for="(item, index) in items" :key="index"
    :title="item.title"
    :description="item.description"
    :price="item.price"
    :discount="item.discount"
    :discount-value="item.discountValue"
    @selectItem="addItem"
  />
</template>

<script lang="ts" setup>
import ItemDetail from './ItemDetail.vue'
import { Item } from './ItemDetail.vue';

const emit = defineEmits<{
  (event: 'addItem', item: Item):void
}>();

const addItem = (item : Item)=> {
  emit('addItem', item);
}

let items = [
  {
    title : 'Papas fritas',
    description : 'Papas a la francesa aderezo normal',
    price : 3,
    discount : false,
    discountValue : 0 
  },
  {
    title : 'Hamburguesa sencilla',
    description : 'Hamburguesa de la casa con 1/4 de libra de carne, vegetales y aderezos de la casa',
    price : 5,
    discount : false,
    discountValue : 0 
  },
  {
    title : 'Hamburguesa especial',
    description : 'Hamburguesa doble carne, vegetales salteados con vino, queso americano y salsas de la casa',
    price : 10,
    discount : true,
    discountValue : 15 
  },
  {
    title : 'Promo pareja',
    description : 'Combo de 2 hamburguesas sencillas mas 2 adiciones de papas y 2 bebidas a elección',
    price : 20,
    discount : true,
    discountValue : 20 
  },
  {
    title : 'Promo pareja',
    description : 'Combo de 2 hamburguesas sencillas mas 2 adiciones de papas y 2 bebidas a elección',
    price : 20,
    discount : true,
    discountValue : 20 
  },
  {
    title : 'Promo pareja',
    description : 'Combo de 2 hamburguesas sencillas mas 2 adiciones de papas y 2 bebidas a elección',
    price : 20,
    discount : true,
    discountValue : 20 
  },
  {
    title : 'Promo pareja',
    description : 'Combo de 2 hamburguesas sencillas mas 2 adiciones de papas y 2 bebidas a elección',
    price : 20,
    discount : true,
    discountValue : 20 
  },
  {
    title : 'Promo pareja',
    description : 'Combo de 2 hamburguesas sencillas mas 2 adiciones de papas y 2 bebidas a elección',
    price : 20,
    discount : true,
    discountValue : 20 
  }
]

</script>

<style>

</style>