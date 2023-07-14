<template>
<header>
  <h1 class="title">Facturador</h1>
</header>
<hr/>
<div class="main-screen">
  <section class="bill">
    <div class="bill-items-section">
      <ul class="displayed-items">
        <li>
          Descripcion
          <span class="item-unit-price">Precio</span>
        </li>
        <BillItem v-for="(item, index) in selectedItemList"
        :key="index"
        :title="item.title"
        :price="item.price"
        @delete-item="deleteItem(index)"
        />
      </ul>
    </div>
    <div class="bill-computed-section">
      <ul class="subtotal-section">
        <li>
          Subtotal:
          <span class="computed-section-value">$ {{ subtotal.toFixed(2) }}</span>
        </li>
        <li>
          Descuentos:
          <span class="computed-section-value">$ {{ discounts.toFixed(2) }}</span>
        </li>
        <li>
          Impuestos (19%):
          <span class="computed-section-value">$ {{ taxes.toFixed(2) }}</span>
        </li>
      </ul>
      <div class="total-section">
        Total a pagar: 
        <span class="computed-section-value">$ {{ total.toFixed(2) }}</span>
      </div>
    </div>
  </section>
  <div class="item-board">
    <ListItem
    @add-item="addItem"
    />
  </div>
  
</div>

</template>

<script lang="ts" setup>
import { Ref, ref, computed } from 'vue';
import ListItem from './components/ListItem.vue';
import { Item } from './components/ItemDetail.vue'
import BillItem from './components/BillItem.vue';

let selectedItemList: Ref<Array<Item>> = ref([])

const addItem = (item : Item)=>{
  selectedItemList.value.push(item);
}

const deleteItem = function(index: number){
  console.log('Se ha eliminado el item: ', selectedItemList.value[index].title);
  selectedItemList.value.splice(index, 1);
 
}

let subtotal = computed(()=>{
  let sum = 0
  selectedItemList.value.map((item)=>{
    sum += item.price;
  });
  return sum
})

let discounts = computed(()=>{
  let sum = 0
  selectedItemList.value.map((item)=>{
    if(item.discount){
      sum += (item.price*item.discountValue)/100;
    }
  });
  return sum
})

let taxes = computed(()=>{
  let sum = 0;
  sum += (subtotal.value - discounts.value)*0.19;
  return sum
})

let total = computed(()=>{
  let sum = 0;
  sum += subtotal.value - discounts.value + taxes.value;
  return sum
})

</script>

<style>
.title {
  width: 100%;
  text-align: center;
}

/* Cuadro global de la factura */
.main-screen {
  display: grid;
  grid-template-columns: 45% 55%;

  width: 500px;
  height: 500px;
  margin: 0 auto;
  padding: 2px;
  border: 3px solid black;
}

/* Lado izquierdo de la factura */
.bill {
  display: grid;
  grid-template-rows: 80% 20%;
  margin: 0px;
  overflow: scroll;
}

/* Detalle de items del lado izquierdo de la factura */
.bill-items-section {
  padding: 4px;  
  
}

.displayed-items {
  display: grid;
  grid-template-rows: auto;
  padding: 0;
  margin: 0;
  list-style: none;
}

.displayed-items li {
  padding: 5px;
}

.item-unit-price {
  float: right;
  border-left: 1px solid black;
  padding-left: 3px;
}

.displayed-items li:last-child {
  border-bottom: 1px solid black;
}

/* Sección de computo del lado izquierdo de la factura */
.bill-computed-section {
  display: grid;
  grid-template-rows: 70% 30%;
  border: 3px solid black;
  padding: 4px;
}

.subtotal-section {
  display: grid;
  grid-template-rows: auto auto auto;
  list-style: none;
  margin: 0;
  padding: 0;
  
}

.total-section {
  padding-top: 7px;
  border-top: 1px solid black;
}

.computed-section-value {
  float: right;
  margin-right: 5px;
}

.item-board {
  display: grid;
  grid-template-columns: 50% 50%;
  padding: 0px 5px;
  row-gap: 5px;
  column-gap: 5px;
  overflow-x: hidden;
}

</style>
