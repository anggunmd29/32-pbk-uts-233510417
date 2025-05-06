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

const removeItem = (index) => {
  shoppingItems.value.splice(index, 1);
};

const togglePurchased = (index) => {
  shoppingItems.value[index].purchased = !shoppingItems.value[index].purchased;
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
        <button @click="removeItem(index)" class="btn-delete">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<style>
.shopping-container {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
}

.input-field {
  padding: 8px;
  width: 70%;
  margin-right: 10px;
}

.btn-add {
  padding: 8px 15px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
}

.item-list {
  list-style: none;
  padding: 0;
  margin-top: 20px;
}

.item {
  padding: 10px;
  border: 1px solid #ddd;
  margin-bottom: 5px;
  display: flex;
  align-items: center;
}
.btn-delete {
  padding: 5px 10px;
  background-color: #f44336;
  color: white;
  border: none;
  cursor: pointer;
  margin-left: auto;
}
.item.purchased {
  text-decoration: line-through;
  color: #888;
}

.item input[type="checkbox"] {
  margin-right: 10px;
}
</style>