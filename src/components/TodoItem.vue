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
