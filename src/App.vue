<script setup>
import { ref, computed } from "vue";

const todos = ref([
  { id: 1, text: "Learn about ref and reactive state", done: true },
  { id: 2, text: "Understand computed properties", done: false },
]);

const remainingCount = computed(
  () => todos.value.filter((todo) => !todo.done).length,
);
</script>

<template>
  <main class="app">
    <h1>Vue 3 basics</h1>

    <ul class="todo-list">
      <li v-for="todo in todos" :key="todo.id">
        {{ todo.text }}
      </li>
    </ul>
  </main>
  <footer class="app__footer">
    {{ remainingCount }} task{{ remainingCount > 1 ? "s" : "" }} remaining
  </footer>
</template>

<style scoped>
.app {
  max-width: 480px;
  margin: 0 auto;
  padding: 2.5rem 1.5rem;
}
</style>
