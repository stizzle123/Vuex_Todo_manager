<template>
  <div>
    <h1>{{ msg }}</h1>
    <div class="legend">
      <span>Double click to mark as complete</span>
      <span>
        <span class="incomplete-box"></span> = Incomplete
      </span>
      <span>
        <span class="complete-box"></span> = Complete
      </span>
    </div>
    <div class="todos">
      <div
        class="todo"
        @dblclick="onDblclick(todo)"
        v-for="todo in allTodos"
        :key="todo.id"
        :class="{'is-complete': todo.completed}"
      >
        {{ todo.title }}
        <i @click="deleteTodo(todo.id)" class="fas fa-trash-alt"></i>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";
export default {
  name: "Todos",
  props: {
    msg: String
  },
  methods: {
    ...mapActions(["fetchTodos", "deleteTodo", "updateTodos"]),
    onDblclick(todo) {
      const updTodo = {
        id: todo.id,
        title: todo.title,
        completed: !todo.completed
      };

      this.updateTodos(updTodo);
    }
  },
  computed: mapGetters(["allTodos"]),
  created() {
    this.fetchTodos();
  }
};
</script>

<style scoped>
h1 {
  font-weight: 300;
}

span {
  font-size: 0.8rem;
}

.todos {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
}

.todo {
  border: 1px solid #ccc;
  background: #41b883;
  padding: 1rem;
  border-radius: 5px;
  text-align: center;
  position: relative;
  cursor: pointer;
  /* transition: all 0.3s ease; */
}

i {
  position: absolute;
  bottom: 10px;
  right: 10px;
  color: #fff;
  cursor: pointer;
}

.legend {
  display: flex;
  justify-content: space-around;
  margin-bottom: 1rem;
}

.complete-box {
  display: inline-block;
  width: 10px;
  height: 10px;
  background: #35495e;
  border: 2px solid #fff;
  border-radius: 50%;
  box-shadow: 0 0 3px rgba(0, 0, 0, 0.4);
}
.incomplete-box {
  display: inline-block;
  width: 10px;
  height: 10px;
  background: #41b883;
  border: 2px solid #fff;
  border-radius: 50%;
  box-shadow: 0 0 3px rgba(0, 0, 0, 0.4);
}

.is-complete {
  background: #35495e;
  color: #fff;
}

@media (max-width: 767px) {
  .todos {
    grid-template-columns: 1fr;
  }
}
</style>
