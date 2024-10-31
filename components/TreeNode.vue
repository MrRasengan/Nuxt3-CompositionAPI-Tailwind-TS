<template>
  <div v-if="node">
    <div @click="toggleChildren" class="cursor-pointer">
      {{ node.locale[locale]?.cg_name || fallbackName }} ({{ breadcrumbs }})
    </div>
    <a :href="node.locale[locale]?.link || ''" target="_blank" class="text-blue-500 underline">Ссылка</a>
    <div v-if="showChildren" class="ml-4">
      <TreeNode
        v-for="child in node.childs"
        :key="child.id"
        :node="child"
        :locale="locale"
        :parentPath="[...parentPath, node.locale[locale]?.cg_name || fallbackName]"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import { defineProps } from 'vue';

interface Locale {
  cg_name: string;
  link: string;
}

interface Node {
  id: number;
  locale: Record<string, Locale>;
  childs: Node[];
}

const props = defineProps<{
  node: Node;
  locale: string;
  parentPath?: string[];
}>();

const showChildren = ref(false);
const toggleChildren = () => {
  showChildren.value = !showChildren.value;
};

const breadcrumbs = computed(() => {
  const pathNames = [...(props.parentPath || []), props.node.locale[props.locale]?.cg_name || ''];
  return pathNames.join(' -> ');
});

const fallbackName = Object.values(props.node.locale)[0]?.cg_name || 'Unnamed';
</script>

<style scoped>
/* Ваши стили */
</style>
