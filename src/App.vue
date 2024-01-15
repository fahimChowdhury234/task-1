<script setup>
import { ref } from "vue";
import CreateStoreList from "./components/CreateStoreList.vue";
import DataList from "./components/DataList.vue";
const dataList = ref([
  { name: "Task 1", time: 60 },
  { name: "Task 2", time: 40 },
  { name: "Task 3", time: 50 },
]);
const openModal = (e) => {
  isOpen.value = e;
};
const closeModal = (e) => {
  console.log(e);
  isOpen.value = e;
};
const addDataToList = (e) => {
  console.log(e);
  dataList.value.push(e);
};
const removeData = (e) => {
  dataList.value.splice(e, 1);
};
const isOpen = ref(false);
</script>

<template>
  <div class="container mx-auto">
    <data-list :dataList="dataList" @openModal="openModal" @removeData="removeData" />

    <CreateStoreList @addDataToList="addDataToList" :isOpen="isOpen" @closeModal="closeModal" />

  </div>
</template>

<style scoped></style>
