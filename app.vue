<script setup>
import { ref } from 'vue'

const msg = ref('Hello World!')

const items = ref([])

let ids = ref(0)

const newItem = ref('')
const nb = ref()
const urgent = ref(false)

const addItem = ()=>{
  if(newItem.value){
    items.value.push({idActive: ids.value,label: newItem.value, number: nb.value,active: false, purchased: false, highPriority: false})
    nb.value = ''
    newItem.value = ''
    ids.value++
  }
}

const cancel = (itemId)=>{
  for (let i=0;i< items.value.length;i++){
    if(itemId === items.value[i].idActive){
      items.value.splice(i,1)
    }
  }
}

function showDelete(){
  this.items.value.active = !this.items.value.active
}

const togglePurchased = (item) =>{
  item.purchased = !item.purchased
}

const togglehighPriority = (item) =>{
  item.purchased = !item.purchased
}

// ids.value = items.value[items.value.length - 1].id +1
</script>

<template>
  <h1>{{ msg }}</h1>

  <input type="number" v-model="nb" v-on:keyup.="" placeholder="How many" />
  <input type="text" v-model="newItem" v-on:keyup.="" placeholder="Add an item" />
  <button v-bind:disabled="!newItem" v-on:click="addItem">Add item</button>

  <ul>
    <li 
      v-for="({idActive, label, number,active, purchased, highPriority},index) in items" 
      key="id" @mouseup="showDelete" 
      class="static-class"
      :class="[
        purchased ? 'strikeout text-gray': 'underlined',
        highPriority ? 'priority': ''
      ]"
      @click="togglePurchased(items[index])"
    >
      {{number +' '+ label}} 
      <button v-show="active" @click="cancel(idActive)" class="deleteBtn"> X</button>
    </li>
  </ul>
  <p v-if="!items.length">Nothing to see here</p>

<h1>{{ids}}</h1>
</template>

<style>
ul{
  list-style: none;
  padding: 0;
  cursor: pointer;
}

body{
  position: absolute;
  top: 30%;
  left: 15%;
  width: 400px;
  height: auto;
  background-color: #ffffff;
  padding: 20px 40px;
  box-shadow: 0 1px 8px 0px rgb(2, 0, 0,0.2);
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.deleteBtn{
  background: transparent;
  border: none;
  cursor: pointer;
  color: red;
  font-weight: bold;
  font-size: 19px;
}

.strikeout{
  text-decoration-line: line-through;
}

.priority{
  font-weight: bold;
  color: orange;
}

.text-gray{
  color: #818181;
}
</style>

