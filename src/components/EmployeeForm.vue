<template>
    <div class="employee-form">
      <h2>{{ isEditing ? 'Cập nhật nhân viên' : 'Thêm mới nhân viên' }}</h2>
      <base-input v-model="employee.name" label="Tên"></base-input>
      <base-input v-model="employee.email" label="Email" type="email"></base-input>
      <base-input v-model="employee.birthDate" label="Ngày sinh" type="date"></base-input>
      <base-button @click="saveEmployee">
        {{ isEditing ? 'Cập nhật' : 'Thêm nhân viên' }}
      </base-button>
      <base-button @click="closeForm">Đóng</base-button>
    </div>
  </template>
  
  <script setup>
  import { defineProps, defineEmits, reactive, watch } from 'vue';
  import BaseInput from './BaseInput.vue';
  import BaseButton from './BaseButton.vue';
  
  const props = defineProps({
    employeeData: Object,
    isEditing: Boolean
  });
  
  const emit = defineEmits(['save', 'close']);
  const employee = reactive({
    name: '',
    email: '',
    birthDate: ''
  });
  
  watch(() => props.employeeData, (newVal) => {
    Object.assign(employee, newVal);
  }, { immediate: true });
  
  const saveEmployee = () => {
    if (!employee.name || !employee.email) {
      alert('Tên và email không được để trống');
      return;
    }
    if (new Date(employee.birthDate) > new Date()) {
      alert('Ngày sinh không được lớn hơn ngày hiện tại');
      return;
    }
    emit('save', employee);
  };
  
  const closeForm = () => {
    emit('close');
  };
  </script>
  
  <style scoped>
  .employee-form {
    background-color: #f9f9f9;
    padding: 20px;
    border-radius: 10px;
  }
  </style>
  