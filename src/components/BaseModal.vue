<template>
    <div class="modal" v-if="visible">
      <div class="modal-content">
        <slot></slot>
        <div class="actions">
          <base-button @click="cancel">Hủy</base-button>
          <base-button @click="confirm">Xóa</base-button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps, defineEmits } from 'vue';
  import BaseButton from './BaseButton.vue';
  
  const props = defineProps({
    visible: Boolean
  });
  
  const emit = defineEmits(['cancel', 'confirm']);
  
  const cancel = () => {
    emit('cancel');
  };
  
  const confirm = () => {
    emit('confirm');
  };
  </script>
  
  <style scoped>
  .modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgba(0, 0, 0, 0.5);
  }
  
  .modal-content {
    background: white;
    padding: 20px;
    border-radius: 8px;
  }
  </style>
  