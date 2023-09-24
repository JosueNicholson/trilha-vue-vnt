<script setup>
import { onMounted, ref } from "vue";
import CategoryList from "./components/CategoryList.vue"
import data from "./data.json"

onMounted(() => categories.value = data.categories)

const categories = ref([])

</script>

<template>
  <div class="page-wrapper">
    <h1>Você ainda não Vue</h1>

    <div class="categories-wrapper">
      <category-list v-for="(category, index) in categories" :key="index" :category-name="category"/>
    </div>
  </div>
</template>

<style scoped>
.categories-wrapper {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
}
</style>
