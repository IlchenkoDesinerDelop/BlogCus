<script setup>
import { ref } from "vue";
</script>

<template>
    <div class="container">
        <ul class="horizontal-menu">
            <li>Main</li>
            <li>Contact</li>
        </ul>
    </div>
</template>

<style scoped>
.container {
  background-color: #837ad1; /* Темный фон для меню */
    position: relative; /* Делаем контейнер позиционируемым */
    padding: 10px; /* Добавляем отступы вокруг контейнера */
}

.horizontal-menu {
    display: flex; /* Размещение элементов в строку */
    list-style: none; /* Удаление маркеров списка */
    padding: 0; /* Удаление отступов */
    justify-content: flex-end; /* Выравнивание элементов по правому краю */
    margin: 0; /* Удаление отступа у меню */
    background-color: #837ad1; /* Темный фон для меню */
    border-radius: 5px; /* Закругленные углы */
}

.horizontal-menu li {
    margin-right: 20px; /* Отступ между элементами */
    color: white; /* Цвет текста */
    cursor: pointer; /* Указатель при наведении */
    padding: 10px 15px; /* Добавляем отступы внутри элементов */
    transition: background-color 0.3s; /* Плавный переход для фона */
}

.horizontal-menu li:hover {
    background-color: #34495e; /* Цвет фона при наведении */
    border-radius: 5px; /* Закругление углов при наведении */
}
</style>