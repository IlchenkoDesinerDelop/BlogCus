<template>
    <div>
      <h3>Редактировать пост</h3>
      <input v-model="title" placeholder="Заголовок рецепта" />
      <textarea v-model="content" placeholder="Содержимое рецепта"></textarea>
  
      <h4>Ингредиенты</h4>
      <div v-for="(ingredient, index) in ingredients" :key="index" class="ingredient">
        <input v-model="ingredient.name" placeholder="Ингредиент" />
        <input v-model="ingredient.amount" placeholder="Количество" />
      </div>
      <button @click="addIngredient">Добавить ингредиент</button>
  
      <h4>Шаги</h4>
      <input v-model="newStep" placeholder="Шаг" />
      <button @click="addStep">Добавить шаг</button>
  
      <button @click="submitEdit">Сохранить изменения</button>
      <button @click="$emit('closeEdit')">Отмена</button>
    </div>
  </template>
  
  <script setup>
  import { ref, defineProps, defineEmits } from 'vue';
  
  const props = defineProps({
    title: String,
    content: String,
    ingredients: Array,
    steps: Array,
    index: Number
  });
  
  const emit = defineEmits();
  
  const title = ref(props.title);
  const content = ref(props.content);
  const ingredients = ref([...props.ingredients]);
  const steps = ref([...props.steps]);
  const newStep = ref('');
  
  // Добавление ингредиента
  const addIngredient = () => {
    ingredients.value.push({ name: '', amount: '' });
  };
  
  // Добавление шага
  const addStep = () => {
    if (newStep.value) {
      steps.value.push(newStep.value);
      newStep.value = ''; // Сброс поля
    }
  };
  
  // Подтверждение редактирования поста
  const submitEdit = () => {
    emit('updatePost', {
      index: props.index,
      title: title.value,
      content: content.value,
      ingredients: ingredients.value,
      steps: steps.value
    });
  };
  </script>
  
  <style scoped>
  .ingredient {
    display: flex;
    margin-bottom: 10px;
  }
  input, textarea {
    width: 100%;
    margin-bottom: 10px;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  button {
    margin-top: 10px;
  }
  </style>