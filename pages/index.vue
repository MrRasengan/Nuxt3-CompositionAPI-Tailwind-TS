<template>
  <div class="p-4">
    <select v-model="selectedLocale" @change="changeLocale" class="mb-4">
      <option value="ru">Русский</option>
      <option value="en">English</option>
      <option value="fr">Français</option>
    </select>

    <div v-if="category">
      <TreeNode
        :node="category"
        :locale="selectedLocale"
        :parentPath="[]"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import TreeNode from '../components/TreeNode.vue';

const selectedLocale = ref('ru');
const category = ref(null);

// Функция для загрузки данных из JSON
const loadCategory = async () => {
  const response = await fetch('../public/task.json');
  const data = await response.json();
  category.value = data;
};

// Функция для изменения локали
const changeLocale = () => {
  // Здесь можно добавить дополнительные действия при изменении языка, если нужно
};

onMounted(loadCategory);
</script>

<style scoped>
/* Ваши стили */
</style>
