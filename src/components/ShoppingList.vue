<script setup>
import { ref } from 'vue';

const shoppingItems = ref([]);
const newItem = ref('');
const showOnlyPending = ref(false);

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

const filteredItems = () => {
  return showOnlyPending.value
    ? shoppingItems.value.filter(item => !item.purchased)
    : shoppingItems.value;
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

    <label class="filter-checkbox">
      <input type="checkbox" v-model="showOnlyPending" />
      Tampilkan hanya item yang belum dibeli
    </label>

    <ul class="item-list">
      <li
        v-for="(item, index) in filteredItems()"
        :key="index"
        class="item"
        :class="{ purchased: item.purchased }"
      >
        <input
          type="checkbox"
          :checked="item.purchased"
          @change="togglePurchased(index)"
        />
        <span>{{ item.text }}</span>
        <button @click="removeItem(index)" class="btn-delete">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #946a6a;
}

#app {
  max-width: 600px;
  margin: 40px auto;
  padding: 20px;
  background-color: rgb(200, 161, 161);
  border-radius: 12px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.title {
  font-family: "Winky Rough", sans-serif;
  text-align: center;
  color: #5b3737;
  margin-bottom: 30px;
  font-size: 40px;
}

.shopping-container {
  display: flex;
  flex-direction: column;
}

.input-field {
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 6px;
  margin-bottom: 10px;
}

.btn-add {
  font-family: "Winky Rough", sans-serif;
  padding: 10px;
  background-color: #885656;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  margin-bottom: 15px;
  font-weight: bold;
}

.btn-add:hover {
  background-color: #477f54;
}

.filter-checkbox {
  margin-bottom: 20px;
  font-size: 16px;
  color: #4d4c4c;
  font-family:"Varela Round", sans-serif;
}

.item-list {
  font-family: "Winky Rough", sans-serif;
  list-style: none;
  padding: 0;
  font-size: 20px;
}

.item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid #eee;
}

.item input[type='checkbox'] {
  margin-right: 10px;
}

.item span {
  flex-grow: 1;
}

.item.purchased span {
  text-decoration: line-through;
  color: rgb(74, 35, 35);
}

.btn-delete {
  font-family: "Winky Rough", sans-serif;
  background-color: #5b3737;
  color: white;
  border: none;
  border-radius: 6px;
  padding: 6px 12px;
  cursor: pointer;
}

.btn-delete:hover {
  background-color: #91242e;
}
</style>