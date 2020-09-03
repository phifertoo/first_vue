<template>
  <div>
    <!-- need unique value -->
    <div v-bind:key="todo.id" v-for="todo in todos">
      <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)" />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  // name of component
  name: "Todos",
  components: {
    //   components contained in the this component
    TodoItem,
  },
  //   props received from parent component
  props: ["todos"],
};
</script>

<style scoped>
</style>