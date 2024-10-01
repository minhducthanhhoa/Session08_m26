<template>
    <button @click="handleClick" class="base-button">
      <slot></slot>
    </button>
  </template>
  
  <script setup>
  import { defineEmits } from 'vue';
  
  const emit = defineEmits(['click']);
  
  const handleClick = () => {
    emit('click');
  };
  </script>
  
  <style scoped>
  .base-button {
    padding: 10px 20px;
    border: none;
    background-color: #42b983;
    color: white;
    cursor: pointer;
    border-radius: 5px;
  }
  </style>
  