<template>
    <div>
      <h3>Удалить пост</h3>
      <p>Вы уверены, что хотите удалить "{{ title }}"?</p>
      <button @click="confirmDelete">Удалить</button>
      <button @click="$emit('closeDelete')">Отмена</button>
    </div>
  </template>
  
  <script setup>
  import { defineProps, defineEmits } from 'vue';
  
  const props = defineProps({
    title: String
  });
  
  const emit = defineEmits();
  
  const confirmDelete = () => {
    emit('deletePost');
  };
  </script>
  
  <style scoped>
  button {
    margin-top: 10px;
  }
  </style>