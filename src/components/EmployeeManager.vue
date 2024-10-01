<template>
    <div class="employee-manager">
      <base-button @click="openForm">Thêm mới nhân viên</base-button>
      <employee-list :employees="employees" @edit="editEmployee" @delete="confirmDelete"></employee-list>
  
      <employee-form v-if="showForm" 
                     :employeeData="currentEmployee" 
                     :isEditing="isEditing" 
                     @save="handleSave" 
                     @close="closeForm"></employee-form>
  
      <base-modal v-if="showDeleteModal" 
                  @cancel="cancelDelete" 
                  @confirm="deleteEmployee">Bạn có chắc chắn muốn xóa không?</base-modal>
    </div>
  </template>
  
  <script setup>
  import { ref, reactive, onMounted } from 'vue';
  
  const employees = ref([]);
  const showForm = ref(false);
  const showDeleteModal = ref(false);
  const isEditing = ref(false);
  const currentEmployee = reactive({ name: '', email: '', birthDate: '' });
  let employeeToDelete = null;
  
  const loadEmployees = () => {
    const storedEmployees = JSON.parse(localStorage.getItem('employees')) || [];
    employees.value = storedEmployees;
  };
  
  const saveEmployees = () => {
    localStorage.setItem('employees', JSON.stringify(employees.value));
  };
  
  const openForm = () => {
    Object.assign(currentEmployee, { name: '', email: '', birthDate: '' });
    isEditing.value = false;
    showForm.value = true;
  };
  
  const closeForm = () => {
    showForm.value = false;
  };
  
  const handleSave = (employee) => {
    if (isEditing.value) {
      const index = employees.value.findIndex(e => e.id === employee.id);
      employees.value.splice(index, 1, employee);
    } else {
      employee.id = Date.now();
      employees.value.push(employee);
    }
    saveEmployees();
    closeForm();
  };
  
  const editEmployee = (employee) => {
    Object.assign(currentEmployee, employee);
    isEditing.value = true;
    showForm.value = true;
  };
  
  const confirmDelete = (id) => {
    employeeToDelete = id;
    showDeleteModal.value = true;
  };
  
  const deleteEmployee = () => {
    employees.value = employees.value.filter(e => e.id !== employeeToDelete);
    saveEmployees();
    showDeleteModal.value = false;
  };
  
  const cancelDelete = () => {
    showDeleteModal.value = false;
  };
  
  onMounted(() => {
    loadEmployees();
  });
  import EmployeeList from './EmployeeList.vue';
  </script>
  
  <style scoped>
  .employee-manager {
    padding: 20px;
  }
  </style>
  