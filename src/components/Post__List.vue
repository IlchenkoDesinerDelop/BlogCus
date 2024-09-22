<template>
    <PostManager v-slot="{ posts, addPost, updatePost, deletePost }">
        <div>
            <h1 class="post-title">Список рецептов</h1>
            <CreateRecipe @createPost="addPost" />

            <div v-for="(post, index) in posts" :key="index" class="post">
                <h2 class="post-title" @click="togglePost(index)">{{ post.title }}</h2>
                <div v-if="isOpen === index" class="post-content">
                    <h4>Ингредиенты</h4>
                    <table>
                        <thead>
                            <tr>
                                <th>Ингредиент</th>
                                <th>Количество</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(ingredient, i) in post.ingredients" :key="i">
                                <td>{{ ingredient.name }}</td>
                                <td>{{ ingredient.amount }}</td>
                            </tr>
                        </tbody>
                    </table>

                    <h4>Шаги</h4>
                    <ol>
                        <li v-for="(step, i) in post.steps" :key="i">{{ step }}</li>
                    </ol>

                    <button @click="startEditing(post, index)">Редактировать</button>
                    <button @click="startDeleting(post)">Удалить</button>
                </div>
            </div>

            <EditPost 
                v-if="editingPost" 
                :title="editingPost.title" 
                :content="editingPost.content" 
                :ingredients="editingPost.ingredients" 
                :steps="editingPost.steps" 
                :index="editingPostIndex" 
                @updatePost="updatePost" 
                @closeEdit="closeEdit" 
            />
            <DeletePost 
                v-if="deletingPost" 
                :title="deletingPost.title" 
                @deletePost="deletePost" 
                @closeDelete="closeDelete" 
            />
        </div>
    </PostManager>
</template>

<script setup>
import { ref } from 'vue';
import CreateRecipe from './Action__Posts/CreateRecipe.vue'; // Исправлен путь
import EditPost from './Action__Posts/EditPost.vue'; 
import DeletePost from './Action__Posts/DeletePost.vue'; 
import PostManager from './PostManager.vue'; // Исправлен путь

const isOpen = ref(null);
const editingPost = ref(null);
const editingPostIndex = ref(null);
const deletingPost = ref(null);

// Функция для переключения поста
const togglePost = (index) => {
    isOpen.value = isOpen.value === index ? null : index; 
};

// Начало редактирования поста
const startEditing = (post, index) => {
    editingPost.value = post;
    editingPostIndex.value = index;
};

// Обновление поста
const updatePost = (updatedPost) => {
    posts.value[updatedPost.index] = updatedPost;
    editingPost.value = null;
    editingPostIndex.value = null;
};

// Закрытие формы редактирования
const closeEdit = () => {
    editingPost.value = null;
    editingPostIndex.value = null;
};

// Начало удаления поста
const startDeleting = (post) => {
    deletingPost.value = post;
};

// Удаление поста
const deletePost = () => {
    const index = posts.value.indexOf(deletingPost.value);
    if (index !== -1) {
        posts.value.splice(index, 1);
    }
    deletingPost.value = null;
};

// Закрытие формы удаления
const closeDelete = () => {
    deletingPost.value = null;
};
</script>

