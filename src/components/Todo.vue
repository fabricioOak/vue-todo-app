<template>
  <div>
    <div class="flex justify-between items-center">
      <div class="text-gray-500 mb-2">Created at: {{ todo.createdAt }}</div>
      <div v-show="todo.done" class="text-gray-500 mb-2">
        Finished at: {{ todo.finishedAt }}
      </div>
    </div>
    <div class="todo">
      <div :class="`${todo.done ? 'is-completed' : ''}`" class="text-2xl">
        {{ todo.content }}
      </div>
      <div class="flex justify-center">
        <button
          @click="toggleDone"
          class="button px-2 transiton-all duration-200 hover:bg-green-600 bg-green-400"
        >
          {{ todo.done ? "Undo" : "Done" }}
        </button>
        <button
          @click="removeTodo"
          class="button px-2 transiton-all duration-200 hover:bg-red-800 bg-red-600 text-white"
        >
          Delete
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  methods: {
    toggleDone() {
      this.$store.commit("toggleTodo", this.todo);
    },
    removeTodo() {
      this.$store.commit("removeTodo", this.todo);
    },
  },
};
</script>

<style lang="postcss" scoped>
.todo {
  @apply flex items-center justify-between bg-gray-800 p-4 rounded-lg mb-4;
}
.button {
  @apply text-white text-lg;
  min-width: fit-content;
}

.is-completed {
  @apply text-gray-400 line-through opacity-50;
}
</style>
