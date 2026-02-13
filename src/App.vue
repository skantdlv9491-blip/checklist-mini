<script setup lang="ts">
import { ref } from "vue";
import CategoryPicker from "./components/CategoryPicker.vue";
import ChecklistEditor from "./components/ChecklistEditor.vue";

type Item = { id: string; categoryId: string; text: string; done: boolean };

const categories = [
  { id: "grocery", label: "장보기" },
  { id: "travel", label: "여행" },
  { id: "baby", label: "아기" },
];

const selectedId = ref("grocery");

const items = ref<Item[]>([]);

const onSelect = (id: string) => {
  selectedId.value = id;
};

const onAdd = (text: string) => {
  items.value.push({
    id: crypto.randomUUID(),
    categoryId: selectedId.value,
    text,
    done: false,
  });
};

const onToggle = (id: string) => {
  const t = items.value.find((v) => v.id === id);
  if (!t) {
    return;
  }
  t.done = !t.done;
};
</script>

<template>
  <h1>Checklist Mini</h1>
  <CategoryPicker
    :categories="categories"
    :selectedId="selectedId"
    @select="onSelect"
  />
  <p>현재 선택: {{ selectedId }}</p>

  <ChecklistEditor
    :items="items"
    :selectedCategoryId="selectedId"
    @add="onAdd"
    @toggle="onToggle"
  />
</template>
