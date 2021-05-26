<template>
  <header class="header">
    <h1>todos</h1>
    <input
      v-model="text"
      @keyup.enter="createTask()"
      class="new-todo"
      placeholder="What needs to be done?"
      autofocus
    />
  </header>
</template>

<script>
import { ref } from "vue";
export default {
  setup(_, ctx) {
    let text = ref("");

    let createTask = () => {
      ctx.emit("create:task", text.value);
      text.value = "";
    };

    return {
      text,
      createTask,
    };
  },
};
</script>

<style lang="scss" scoped>
</style>