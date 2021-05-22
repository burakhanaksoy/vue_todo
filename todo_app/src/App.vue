<template>
  <div class="container-for-todo">
    <h1>Vue 3 Todo App</h1>
    <form class="new-todo-form" @submit.prevent="addNewTodo">
      <label class="new-todo-label">New Todo</label>
      <input v-model="newTodo" class="new-todo-input" />
      <button class="new-todo-button">Add New Todo</button>
    </form>
    <button class="remove-all-todos-button" @click="removeAllTodo">
      Remove All Todo
    </button>
  </div>
  <div class="todo-box" v-for="(todo, index) in todos" :key="todo.id">
    <ul>
      <li
        @click="toggleDone(todo)"
        class="todo-list-item"
        :class="{ done: todo.done }"
      >
        {{ todo.content }}
      </li>
      <button @click="removeToDo(index)">Remove Todo</button>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const todos = ref([]);
    const newTodo = ref("");
    function addNewTodo() {
      todos.value.unshift({
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }

    function removeAllTodo() {
      todos.value = [];
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }
    function removeToDo(index) {
      todos.value.splice(index, 1);
    }
    return {
      addNewTodo,
      newTodo,
      todos,
      toggleDone,
      removeToDo,
      removeAllTodo,
    };
  },
};
</script>

<style>
#app {
  user-select: none;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.new-todo-form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.new-todo-input {
  margin-top: 1rem;
  margin-bottom: 1rem;
  min-width: 20rem;
}
.new-todo-button {
  font-size: 1rem;
  width: 10rem;
  margin-bottom: 1rem;
}
.container-for-todo {
  background-color: aliceblue;
  width: 30rem;
  border: 1px solid;
}

.todo-box-container {
  border: 1px solid;
  margin-top: 1rem;
}
.todo-box {
  width: 30rem;
  border: 1px solid;
  font-size: 1.1rem;
}
.todo-list-item {
  cursor: pointer;
  font-size: 30px;
  list-style-type: none;
}

.done {
  text-decoration: line-through;
}

.remove-all-todos-button {
  font-size: 1rem;
  width: 10rem;
  margin-bottom: 1rem;
}
</style>
