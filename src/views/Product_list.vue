<template lang="">
    <div class="container my-5">
    
        welcome product list
    <table class="table table-hover">
  <thead>
    <tr class="table table-dark table-sm">
      <th>ID</th>
      <th>Title</th>
      <th>Description</th>
      <th>Category</th>
      <th>Price</th>
      <th>Image</th>
    </tr>
  </thead>
  <tbody class="table-group-divider">
    <tr v-for="Item in products" :key="Item.id">
      <td >{{Item.id}}</td>
      <td>{{Item.title}}</td>
      <td>{{Item.description}}</td>
      <td>{{Item.category}}</td>
      <td>{{Item.price}}</td>
    <td>
        <img
            :src="Item.images"
            width="100"
            class="card-img-top"
            alt="Product Image"
            style="object-fit: contain; width: 100%; height: 180px"
          />
    </td>
       </tr>   
  </tbody>
</table>


    </div>
</template>


<script setup>
import { ref, onMounted } from 'vue'

const products = ref([])
const loading = ref(true)
const error = ref(null)

onMounted(async () => {
  try {
    const res = await fetch('https://dummyjson.com/products')
    const data = await res.json()
    products.value = data.products
  } catch (err) {
    error.value = 'โหลดข้อมูลไม่สำเร็จ'
  } finally {
    loading.value = false
  }
})
</script>