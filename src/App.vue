<template>
  <div id="app">
    <div class="container">
      <AddTodo/>
      <FilterTodos/>
      <Todos msg="Todos App"/>
    </div>
  </div>
</template>

<script>
import Todos from "./components/Todos.vue";
import AddTodo from "./components/AddTodo.vue";
import FilterTodos from "./components/FilterTodos.vue";

export default {
  name: "app",
  components: {
    Todos,
    AddTodo,
    FilterTodos
  }
};
</script>

<style>
body {
  font-family: "Oswald", sans-serif, Arial;
  background: #e8f7f0;
  line-height: 1.6;
}

.container {
  margin: auto;
  max-width: 1100px;
  overflow: auto;
  padding: 0 2rem;
}
</style>
