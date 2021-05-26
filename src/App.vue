<template>
  <section class="todoapp">
    <AppHeader v-on:create:task="onTaskCreate($event)"></AppHeader>
    <!-- This section should be hidden by default and shown when there are todos -->
    <section class="main">
      <input id="toggle-all" class="toggle-all" type="checkbox" />
      <label for="toggle-all">Mark all as complete</label>
      <ul class="todo-list">
        <!-- These are here just to show the structure of the list items -->
        <!-- List items should get the class `editing` when editing and `completed` when marked as completed -->
        <li class="completed">
          <div class="view">
            <input class="toggle" type="checkbox" checked />
            <label>Taste JavaScript</label>
            <button class="destroy"></button>
          </div>
          <input class="edit" value="Create a TodoMVC template" />
        </li>
        <li>
          <div class="view">
            <input class="toggle" type="checkbox" />
            <label>Buy a unicorn</label>
            <button class="destroy"></button>
          </div>
          <input class="edit" value="Rule the web" />
        </li>
      </ul>
    </section>
    <!-- This footer should be hidden by default and shown when there are todos -->
    <AppFooter></AppFooter>
  </section>
</template>


<script>
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
import { computed } from "vue";
export default {
  components: {
    AppHeader,
    AppFooter,
  },
  setup() {
    let onTaskCreate = (evt) => {
      console.log(evt);
    };

    return {
      onTaskCreate,
    };
  },
};
</script>

<style lang="scss">
@import "src/scss/main.scss";
</style>
