<!-- top level -->
<!--  has all todos data -->
<!--  passes todos data down thru props -->
<!--  renders todos component and binds todos data as a prop -->

<template>
  <div id="app">
    <Header/>
    <!-- listens for the emitted event add-todo  -->
    <!-- runs addtodo f(x) to add to the todos array -->
    <AddTodoItem v-on:add-todo="addTodo"/>
    <!-- after receiving del-todo from todos, todoitem -->
    <!-- we call deleteTodo here in app -->
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import axios from "axios";

import Todos from "./components/Todos";
import Header from "./components/layout/Header";
import AddTodoItem from "./components/AddTodoItem";

export default {
  name: "app",
  components: {
    Header,
    Todos,
    AddTodoItem
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(res => console.log(res))
        .catch(err => console.log(err));

      // can be supplied in the promise
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(newTodo) {
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title: this.title,
          completed: this.completed
        })
        .then(res => console.log(res))
        .catch(err => console.log(err));

      // can be supplied in the promise
      this.todos = [...this.todos, newTodo];
    }
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then(res => (this.todos = res.data))
      .catch(err => console.log(err));
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
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
