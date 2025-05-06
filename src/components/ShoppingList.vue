<script setup>
import { ref } from 'vue';

const shoppingItems = ref([]);
const newItem = ref('');

const addItem = () => {
  if (newItem.value.trim()) {
    shoppingItems.value.push({ text: newItem.value, purchased: false });
    newItem.value = '';
  }
};
</script>

<template>
<div class="shopping-container">
    <input
      v-model="newItem"
      placeholder="Masukkan item belanja"
      class="input-field"
    />
    <button @click="addItem" class="btn-add">Tambah</button>

    <ul class="item-list">
      <li
        v-for="(item, index) in shoppingItems"
        :key="index"
        class="item"
      >
        <span>{{ item.text }}</span>
      </li>
    </ul>
  </div>
</template>