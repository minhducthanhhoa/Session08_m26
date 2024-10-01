<template>
    <div class="employee-list">
      <table>
        <thead>
          <tr>
            <th>Tên</th>
            <th>Email</th>
            <th>Ngày sinh</th>
            <th>Hành động</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="employee in employees" :key="employee.id">
            <td>{{ employee.name }}</td>
            <td>{{ employee.email }}</td>
            <td>{{ formatDate(employee.birthDate) }}</td>
            <td>
              <button @click="editEmployee(employee)">Sửa</button>
              <button @click="deleteEmployee(employee.id)">Xóa</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script setup>
  import { defineProps, defineEmits } from 'vue';
  
  const props = defineProps({
    employees: Array
  });
  
  const emit = defineEmits(['edit', 'delete']);
  
  const editEmployee = (employee) => {
    emit('edit', employee);
  };
  
  const deleteEmployee = (id) => {
    emit('delete', id);
  };
  
  const formatDate = (date) => {
    const d = new Date(date);
    return d.toLocaleDateString('vi-VN');
  };
  </script>
  
  <style scoped>
  table {
    width: 100%;
    border-collapse: collapse;
  }
  
  th, td {
    padding: 10px;
    border: 1px solid #ccc;
  }
  
  button {
    margin-right: 5px;
    padding: 5px 10px;
    background-color: #42b983;
    color: white;
    border: none;
    cursor: pointer;
  }
  </style>
  