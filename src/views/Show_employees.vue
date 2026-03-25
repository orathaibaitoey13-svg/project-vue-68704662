<template lang="">
    <div class="container my-5">
      <h2>แสดงข้อมูลลูกค้า</h2>
    <table class="table table-hover">
  <thead>
    <tr class="table table-dark table-sm">
      <th>รหัสลูกค้า</th>
      <th>ชื่อ-นามสกุล</th>
      <th>คณะ</th>
      <th>เงินเดือน</th>
      <th>active</th>
      <th>วันที่ทำรายการ</th>
    </tr>
  </thead>
  <tbody class="table-group-divider">
    <tr v-for="Item in employees" :key="employees_id">
      <td >{{Item.emp_id}}</td>
      <td>{{Item.full_name}}</td>
      <td>{{Item.department}}</td>
      <td>{{Item.salary}}</td>
      <td>
       <span v-if="Item.active==1">ปกติ</span>
       <span v-else>ลาออก</span>
      </td>
      <td>{{Item.created_at}}</td>
      
       </tr>   
  </tbody>
</table>


    </div>
</template>


<script setup>
import { ref, onMounted } from 'vue'

const employees = ref([])
const loading = ref(true)
const error = ref(null)

onMounted(async () => {
  try {
    const res = await fetch('http://localhost/project-vue-68704662/php_api/show_employees.php')
    employees.value = await res.json()
    //products.value = data.products
  } catch (err) {
    error.value = 'โหลดข้อมูลไม่สำเร็จ'
  } finally {
    loading.value = false
  }
})
</script>