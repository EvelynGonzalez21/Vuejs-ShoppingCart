<script setup>
import { ref } from 'vue';
const header = ref('App Lista de compras');
const items = ref([
  {id: 1, label: '1 muñeca Ladybug', purchased: true, highPriority : false},
  {id: 2, label: '1  muñeco Catnoa', purchased: false, highPriority: true},
  {id: 3, label: '2 kwamis', purchased: true, highPriority:false}
]);
//Funcion que alternan el estado de compra de un item
const togglepurchased = (item)=>{
  //invertir la propiedad "purchased"
  item.purchased = !item.purchased;
}
// Agregando metodo para guardar nuevo articulo en la lista
const saveItem =() => {
  items.value.push({id: items.value.length + 1, label: newItem.value})
  // Limpiando el contenido de la caja de txt
  newItem.value = "";
};
const newItem = ref('');
const newItemHighPriority = ref(false);
const editing = ref(false);
const doEdit = (edit) => {
  //altero la variable "editing"
  editing.value = edit;
  // Limpiando el inpunt del txt
  newItem.value = "";
};
</script>
<template>
   <div class="header">
    <h1> <i class="material-icons shopping-cart-icon">local_mall</i> {{ header }}</h1>
   <button v-if="!editing" @click="doEdit(true)" class="btn btn-primary"> Agregar articulo.</button>
   <button v-else @click="doEdit(false)" class="btn">Cancelar</button>  
</div>
<!-- <a :href="newItem" como enlazar un producto>
  <i class="material-icons shopping-cart-icon">link</i>
</a> -->
<form v-if="editing" v-on:submit.prevent="saveItem" class="add-item form">
  <!-- Input de Nuevo Articulo -->
  <input v-model.trim="newItem" type="text" placeholder="Ingresar nuevo articulo">
  <!-- Check Boxes -->
  <label>
      <input v-model="newItemHighPriority" 
      type="checkbox">
      Alta Prioridad
    </label>
    {{ newItemHighPriority ? "🔥" : "🧊" }}
    <!-- Boton de UI -->
    <button :disabled="newItem.length == 0" class="btn btn-primary">Salvar Articulo</button>
  </form>
  <ul>
    <li 
    v-for="({ id, label, purchased,highPriority }, index) in items"
     v-bind:key="id"
     :class="{strikeout : purchased, priority: highPriority}"
     @click="togglepurchased(items[index])"
     >
     🎃 {{ label }}
    </li>
  </ul>
  <p v-if="items.length === 0">🥀Lista de compras vacia🥀</p>
  
</template>
<style scoped>
.shopping-cart-icon {
  font-size: 2rem; /* Adjust the font-size value as per your desired size */
}
</style>
