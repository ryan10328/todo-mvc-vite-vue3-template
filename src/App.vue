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
        <li :class="{ completed: item.done }" v-for="(item, index) in filteredTasks" :key="index">
          <div class="view">
            <input class="toggle" type="checkbox" v-model="item.done" />
            <label>{{item?.text}}</label>
            <button class="destroy" @click="removeTask(index)"></button>
          </div>
          <input class="edit" value="Create a TodoMVC template" />
        </li>
      </ul>
    </section>
    <!-- This footer should be hidden by default and shown when there are todos -->
    <AppFooter
      :items-left="itemsLeft"
      v-on:selected:change="onSelectedChange($event)"
      v-on:clear:clicked="onClearClicked()"
    ></AppFooter>
  </section>
</template>


<script>
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";
import { computed, reactive, toRefs, watch, ref } from "vue";
export default {
  components: {
    AppHeader,
    AppFooter,
  },
  setup() {
    const filteredTasks = ref([]);
    const obj = reactive({
      flag: "",
      tasks: [],
    });

    const onTaskCreate = (evt) => {
      obj.tasks.push({
        done: false,
        text: evt,
        id: Date.now(),
      });
    };

    const removeTask = (index) => {
      obj.tasks.splice(index, 1);
    };

    const onSelectedChange = (evt) => {
      obj.flag = evt;
    };

    const onClearClicked = () => {
      obj.tasks = obj.tasks.filter((g) => !g.done);
    };

    watch(obj, (val, newVal) => {
      switch (newVal.flag) {
        case "all":
          filteredTasks.value = obj.tasks;
          return;
        case "active":
          filteredTasks.value = obj.tasks.filter((g) => !g.done);
          return;
        case "completed":
          filteredTasks.value = obj.tasks.filter((g) => g.done);
          return;
      }
    });

    const itemsLeft = computed(() => {
      return obj.tasks.filter((g) => !g.done).length;
    });

    return {
      onTaskCreate,
      onSelectedChange,
      onClearClicked,
      filteredTasks,
      removeTask,
      itemsLeft,
      ...toRefs(obj),
    };
  },
};
</script>

<style lang="scss">
@import "src/scss/main.scss";
</style>
