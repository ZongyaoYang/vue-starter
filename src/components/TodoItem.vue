<script setup>
defineProps({
  todo: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(["toggle", "remove"]);
</script>

<template>
  <li class="todo-item" :class="{ 'todo-item--done': todo.done }">
    <label class="todo-item__label">
      <input
        type="checkbox"
        :checked="todo.done"
        @change="emit('toggle', todo.id)"
      />
      <span>{{ todo.text }}</span>
    </label>
    <button
      type="button"
      class="todo_item__remove"
      aria-label="Remove task"
      @click="emit('remove', todo.id)"
    >
      x
    </button>
  </li>
</template>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 0.75rem;
  padding: 0.6rem 0.75rem;
  border: 1px solid #e5e7eb;
  border-radius: 6px;
}

.todo-item--done {
  text-decoration: line-through;
  color: #9ca3af;
}
</style>
