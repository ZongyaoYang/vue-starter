<script setup>
import { ref, computed } from "vue";
import TodoItem from "./components/TodoItem.vue";

const todos = ref([
  { id: 1, text: "Learn about ref and reactive state", done: true },
  { id: 2, text: "Understand computed properties", done: false },
]);

const remainingCount = computed(
  () => todos.value.filter((todo) => !todo.done).length,
);

const newTodoText = ref("");
let nextId = 3;

function addTodo() {
  const text = newTodoText.value.trim();
  if (!text) return;

  todos.value.push({ id: nextId++, text, done: false });
  nextTodoText.value = "";
}

function toggleTodo(id) {
  const todo = todos.value.find((t) => t.id == id);
  if (todo) {
    todo.done = !todo.done;
  }
}

function removeTodo(id) {
  todos.value = todos.value.filter((t) => t.id !== id);
}
</script>

<template>
  <main class="app">
    <h1>Vue 3 basics</h1>

    <form class="add-form" @submit.prevent="addTodo">
      <input
        v-model="newTodoText"
        type="text"
        placeholder="What do you need to do?"
      />
      <button type="submit">Add</button>
    </form>

    <p v-if="todos.length === 0" class="empty-state">
      Nothing here yet - add your first task above
    </p>

    <ul v-else class="todo-list">
      <TodoItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @toggle="toggleTodo"
        @remove="removeTodo"
      />
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
