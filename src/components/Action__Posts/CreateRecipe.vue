<template>
    <div>
        <button @click="showForm = !showForm">
            {{ showForm ? 'Отмена' : 'Добавить рецепт' }}
        </button>
        <div v-if="showForm" class="create-post-form">
            <input v-model="newTitle" placeholder="Заголовок рецепта" />
            <textarea v-model="newContent" placeholder="Содержимое рецепта"></textarea>
  
            <div>
                <h4>Ингредиенты</h4>
                <input v-model="newIngredient.name" placeholder="Ингредиент" />
                <input v-model="newIngredient.amount" placeholder="Количество" />
                <button @click="addIngredient">Добавить ингредиент</button>
                <table>
                    <thead>
                        <tr>
                            <th>Ингредиент</th>
                            <th>Количество</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(ingredient, i) in ingredients" :key="i">
                            <td>{{ ingredient.name }}</td>
                            <td>{{ ingredient.amount }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
  
            <div>
                <h4>Шаги</h4>
                <input v-model="newStep" placeholder="Шаг" />
                <button @click="addStep">Добавить шаг</button>
                <ol>
                    <li v-for="(step, i) in steps" :key="i">{{ step }}</li>
                </ol>
            </div>
  
            <button @click="submitPost">Добавить</button>
        </div>
    </div>
  </template>
  
  <script setup>
  import { ref, defineEmits } from 'vue';
  
  const emit = defineEmits();
  const showForm = ref(false);
  const newTitle = ref('');
  const newContent = ref('');
  const newIngredient = ref({ name: '', amount: '' });
  const ingredients = ref([]);
  const newStep = ref('');
  const steps = ref([]);
  
  // Добавление ингредиента
  const addIngredient = () => {
      if (newIngredient.value.name && newIngredient.value.amount) {
          ingredients.value.push({ name: newIngredient.value.name, amount: newIngredient.value.amount });
          newIngredient.value = { name: '', amount: '' }; // Сброс поля
      }
  };
  
  // Добавление шага
  const addStep = () => {
      if (newStep.value) {
          steps.value.push(newStep.value);
          newStep.value = ''; // Сброс поля
      }
  };
  
  // Добавление нового поста
  const submitPost = () => {
      if (newTitle.value && newContent.value) {
          emit('createPost', {
              title: newTitle.value, 
              content: newContent.value, 
              ingredients: [...ingredients.value], // Сохраняем ингредиенты
              steps: [...steps.value] // Сохраняем шаги
        });
        newTitle.value = ''; // Сброс полей
        newContent.value = '';
        ingredients.value = []; // Сброс ингредиентов
        steps.value = []; // Сброс шагов
        showForm.value = false; // Закрываем форму
    } else {
        alert('Пожалуйста, заполните все поля.'); // Сообщение об ошибке
    }
};
</script>
