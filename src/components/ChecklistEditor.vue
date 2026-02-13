<script setup lang="ts">
import { ref } from "vue";
type Item = { id: string; categoryId: string; text: string; done: boolean };
const text = ref("");

const props = defineProps<{
  items: Item[];
  selectedCategoryId: string;
}>();

const emit = defineEmits<{
  (e: "add", text: string): void;
  (e: "toggle", id: string): void;
}>();

const onClick = () => {
  if (!text.value.trim()) {
    return;
  }
  emit("add", text.value.trim());

  text.value = "";
};

const liClick = (id: string) => {
  emit("toggle", id);
};
</script>
<template>
  <div>
    <input
      type="text"
      v-model="text"
      placeholder="할 일 입력"
      @keydown.enter="onClick"
    />
    <button type="button" @click="onClick">추가</button>

    <h2>목록</h2>
    <ul>
      <template v-for="item in props.items" :key="item.id">
        <li
          v-if="item.categoryId === props.selectedCategoryId"
          @click="liClick(item.id)"
          style="cursor: pointer"
        >
          <span v-if="item.done">
            <s>{{ item.text }}</s> ✅
          </span>
          <span v-else>
            {{ item.text }}
          </span>
        </li>
      </template>
    </ul>
  </div>
</template>
