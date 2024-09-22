<template>
    <div>
        <slot :posts="posts" :addPost="addPost" :updatePost="updatePost" :deletePost="deletePost"></slot>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const posts = ref([]);

// Загрузка постов из localStorage
const loadPosts = () => {
    const savedPosts = localStorage.getItem('posts');
    if (savedPosts) {
        posts.value = JSON.parse(savedPosts);
    }
};

// Сохранение постов в localStorage
const savePosts = () => {
    localStorage.setItem('posts', JSON.stringify(posts.value));
};

// Добавление нового поста
const addPost = (newPost) => {
    posts.value.push(newPost);
    savePosts();
};

// Обновление поста
const updatePost = (updatedPost) => {
    posts.value[updatedPost.index] = updatedPost;
    savePosts();
};

// Удаление поста
const deletePost = (index) => {
    posts.value.splice(index, 1);
    savePosts();
};

// Загрузка постов при монтировании компонента
onMounted(() => {
    loadPosts();
});
</script>

