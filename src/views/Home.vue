<template>
  <div id="app">
    {{ msg }}
    <!-- <Header /> -->
    <!-- catch an emit from the Todo child component -->
    <AddTodo v-on:add-todo="addTodo" />
    <!-- v-bind: passes in data into the component -->
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import Todos from "../components/Todos";
// import Header from "../components/layout/Header";
import AddTodo from "../components/AddTodo";
import axios from "axios";

export default {
  name: "Home",
  components: {
    Todos,
    // Header,
    AddTodo,
  },
  // pass in data to the component here
  data() {
    return {
      msg: "hello",
      todos: [
        // { id: 1, title: "Todo One", completed: false },
        // {
        //   id: 2,
        //   title: "Todo Two",
        //   completed: true,
        // },
        // { id: 3, title: "Todo Three", completed: false },
      ],
    };
  },
  methods: {
    deleteTodo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(() => (this.todos = this.todos.filter((todo) => todo.id !== id)))
        .catch((err) => console.log(err));
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;

      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed,
        })
        .then((res) => (this.todos = [...this.todos, res.data]))
        .catch((err) => console.log(err));

      this.todos = [...this.todos, newTodo];
    },
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then((res) => (this.todos = res.data))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
