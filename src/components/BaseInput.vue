<template>
    <div class="base-input">
      <label>{{ label }}</label>
      <input
        :type="type"
        v-model="inputValue"
        @input="handleInput"
      />
    </div>
  </template>
  
  <script setup>
  import { defineProps, defineEmits, ref, watch } from 'vue';
  
  const props = defineProps({
    label: String,
    type: {
      type: String,
      default: 'text',
    },
    value: String,
  });
  
  const emit = defineEmits(['update:value']);
  const inputValue = ref(props.value);
  
  watch(() => props.value, (newValue) => {
    inputValue.value = newValue;
  });
  
  const handleInput = () => {
    emit('update:value', inputValue.value);
  };
  </script>
  
  <style scoped>
  .base-input {
    display: flex;
    flex-direction: column;
    margin-bottom: 15px;
  }
  
  .base-input input {
    padding: 10px;
    border-radius: 4px;
    border: 1px solid #ccc;
  }
  </style>
  