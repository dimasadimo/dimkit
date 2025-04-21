<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'
import ItemsCard from '../cards/ItemsCard.vue'
import { useRoute } from 'vue-router'

const route = useRoute()
let category = ref()
// let items = ref([
//   { id: 1, title: 'Mobile UI Kit', image: 'items-1.jpg', header: 'Mobile UI Kit' },
//   { id: 2, title: 'Online Doctor Consultation', image: 'items-2.jpg', header: 'Website UI Kit' },
//   { id: 3, title: 'Banking Crypto', image: 'items-3.jpg', header: 'Mobile UI Kit' },
// ])
let items = ref()

const getProductData = async () => {
  try {
    const response = await axios.get('http://127.0.0.1:8000/api/categories?id=' + route.params.id)
    items.value = response.data.data.products
    category.value = response.data.data.name
  } catch (error) {
    console.log(error)
  }
}

onMounted(() => {
  getProductData()
})


</script>

<template>
  <div class="container px-4 mx-auto my-16 md:px-12">
    <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">{{ category }}</h2>
    <div class="flex flex-wrap -mx-1 lg:-mx-4">
      <ItemsCard
        v-for="item in items"
        :id="item.id"
        :key="item.id"
        :title="item.name"
        :image="item.thumbnails"
        :header="item.subtitle"
      />
    </div>
  </div>
</template>
