<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'
import CategoriesCard from '../cards/CategoriesCard.vue'

// let categories = ref([
//   { id: 1, title: 'Mobile UI Kit', image: 'categories-1.jpg', count: '731' },
//   { id: 2, title: 'Fonts', image: 'categories-2.jpg', count: '657' },
//   { id: 3, title: 'Icon Set', image: 'categories-3.jpg', count: '83,559' },
//   { id: 4, title: 'Website UI Kit', image: 'categories-4.jpg', count: '4,500' },
// ])

let categories = ref()

const getCategoriesData = async () => {
  try {
    const response = await axios.get('http://127.0.0.1:8000/api/categories')
    categories.value = response.data.data.data
  } catch (error) {
    console.log(error)
  }
}

onMounted(() => {
  getCategoriesData()
})

</script>

<template>
  <div class="container px-4 mx-auto my-16 md:px-12">
    <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">All Categories</h2>
    <div class="flex flex-wrap -mx-1 lg:-mx-4">
      <CategoriesCard
        v-for="category in categories"
        :id="category.id"
        :key="category.id"
        :title="category.name"
        :image="category.thumbnails"
        :count="category.products_count"
      />
    </div>
  </div>
</template>
