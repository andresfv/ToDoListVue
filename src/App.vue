<script setup>
import { ref } from 'vue';

const items = ref([
  { id: 1, label: 'Item 1', hecha: false },
  { id: 2, label: 'Item 2', hecha: false },
  { id: 3, label: 'Item 3', hecha: false },
]);

const newItem = ref('');
const mostrar = ref(false);

const agregaItem = () => {
  items.value.push({
    id: items.value.length + 1,
    label: newItem.value,
    hecha: false,
  });

  newItem.value = '';
};

const mostrarFormulario = () => {
  mostrar.value = !mostrar.value;
  newItem.value = '';
};

const marcar = (item) => {
  item.hecha = !item.hecha;
};

const eliminarItem = (item) => {
  //Preferida para entornos reactivos
  items.value = items.value.filter((i) => i.id !== item.id);

  //const index = items.value.indexOf(item);
  //const index = items.value.findIndex(i => i.id === item.id);//Más seguro
  //if(index !== -1){
  //  items.value.splice(index, 1);
  //}
};
</script>

<template>
  <h1>Shoping List</h1>

  <button v-if="!mostrar" class="btn btn-primary" @click="mostrarFormulario">Editar</button>

  <form v-else class="add-item-form" @submit.prevent="agregaItem">
    <input type="text" v-model.trim="newItem" placeholder="Ingrese un valor" />

    <button :disabled="newItem.length === 0" class="btn btn-primary">Agregar</button>

    <button @click="mostrarFormulario" class="btn btn-primary">Listo</button>
  </form>

  <ul v-if="items.length > 0">
    <div v-for="item in items" :key="item.id">
      <li v-if="!mostrar" @click="marcar(item)" :class="{ strikeout: item.hecha }">
        {{ item.label }}
      </li>

      <input v-if="mostrar" type="text" v-model="item.label" />
      <button v-if="mostrar" @click="eliminarItem(item)">Eliminar</button>
    </div>
  </ul>

  <p v-else>Nada que mostrar</p>
</template>

Spring-MVC-and-Hibernate-Project
