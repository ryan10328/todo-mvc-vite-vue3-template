<template>
  <footer class="footer">
    <!-- This should be `0 items left` by default -->
    <span class="todo-count">
      <strong>{{itemsLeft}}</strong> item left
    </span>
    <!-- Remove this if you don't implement routing -->
    <ul class="filters">
      <li>
        <a :class="{selected: selectedItem === 'all'}" :href="void(0)" @click="check('all')">All</a>
      </li>
      <li>
        <a
          :class="{selected: selectedItem === 'active'}"
          :href="void(0)"
          @click="check('active')"
        >Active</a>
      </li>
      <li>
        <a
          :class="{selected: selectedItem === 'completed'}"
          :href="void(0)"
          @click="check('completed')"
        >Completed</a>
      </li>
    </ul>
    <!-- Hidden if no completed items are left ↓ -->
    <button class="clear-completed" @click="clearComplete">Clear completed</button>
  </footer>
</template>

<script>
import { ref } from "vue";
export default {
  props: {
    itemsLeft: Number,
  },
  setup(props, ctx) {
    const selectedItem = ref("all");
    ctx.emit("selected:change", selectedItem.value);

    const check = (flag) => {
      selectedItem.value = flag;
      ctx.emit("selected:change", selectedItem.value);
    };

    const clearComplete = () => {
      ctx.emit("clear:clicked");
    };

    return {
      selectedItem,
      check,
      clearComplete,
    };
  },
};
</script>

<style lang="scss" scoped>
</style>