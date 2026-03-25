<template lang="">
    <div class="container my-5">
      <h2>แสดงข้อมูลลูกค้า</h2>
    <table class="table table-hover">
  <thead>
    <tr class="table table-dark table-sm">
      <th>รหัสลูกค้า</th>
      <th>ชื่อ</th>
      <th>นามสกุล</th>
      <th>เบอร์โทรศัพท์</th>
      <th>Username</th>
    </tr>
  </thead>
  <tbody class="table-group-divider">
    <tr v-for="Item in customers" :key="customer_id">
      <td >{{Item.customer_id}}</td>
      <td>{{Item.firstName}}</td>
      <td>{{Item.lastName}}</td>
      <td>{{Item.phone}}</td>
      <td>{{Item.username}}</td>
    
       </tr>   
  </tbody>
</table>


    </div>
</template>


<script setup>
import { ref, onMounted } from 'vue'

const customers = ref([])
const loading = ref(true)
const error = ref(null)

onMounted(async () => {
  try {
    const res = await fetch('http://localhost/project-vue-68704662/php_api/show_customer.php')
    customers.value = await res.json()
    //products.value = data.products
  } catch (err) {
    error.value = 'โหลดข้อมูลไม่สำเร็จ'
  } finally {
    loading.value = false
  }
})
</script>