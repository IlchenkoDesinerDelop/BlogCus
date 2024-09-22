<script setup>
import { ref } from "vue";
</script>

<template>
  <footer class="footer">
    <div class="container">
      <p>© 2023 Все права защищены. Телефон: +7 (123) 456-78-90</p>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background-color: #f0f0f0; /* Цвет фона футера */
  padding: 20px; /* Отступ внутри футера */
  text-align: center; /* Выравнивание текста по центру */
  font-size: 0.8em; /* Размер шрифта */
  color: #333; /* Цвет текста */
  position: fixed; /* Фиксируем футер внизу страницы */
  bottom: 0; /* Помещаем футер внизу страницы */
  width: 100%; /* Ширина футера на всю ширину страницы */
  z-index: 1;
}

.container {
  max-width: 960px; /* Максимальная ширина контейнера */
  margin: 0 auto; /* Выравнивание по центру */
}
</style>