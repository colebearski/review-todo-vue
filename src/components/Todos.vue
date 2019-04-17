<!-- for loops (v-for) TODOS data as a TODO -->
<!-- TodoItem binds each TODO data as a prop -->

<template>
  <div>
    <div v-bind:key="todo.id" v-for="todo in todos">
      <!-- after getting passed from todoitem, we're also emitting del-todo to app -->
      <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>
      <!-- {{todo}} -->
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";

export default {
  name: "Todos",
  components: {
    TodoItem
  },
  props: ["todos"]
};
</script>

<style scoped>
</style>


