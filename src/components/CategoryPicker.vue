<script setup lang="ts">
const props = defineProps<{
  categories: { id: string; label: string }[];
  selectedId: string;
}>();

const emit = defineEmits<{
  (e: "select", id: string): void;
}>();

const onClick = (id: string) => {
  emit("select", id);
};
</script>

<template>
  <div v-for="category in props.categories" :key="category.id">
    <button
      type="button"
      @click="onClick(category.id)"
      :aria-pressed="category.id === props.selectedId"
    >
      {{ category.label }}
      <span v-if="category.id === props.selectedId"> ✅</span>
    </button>
  </div>
</template>
