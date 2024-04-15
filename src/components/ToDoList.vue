<template>
  <div class="todo-app">
    <h1>My Todo List</h1>
    <input type="text" v-model="newTodo" placeholder="Add a new todo" />
    <button @click="addTodo">Add</button>
    <ul>
      <li v-for="todo in todos" :key="todo.id">
        <input type="checkbox" v-model="todo.done" />
        <span>{{ todo.text }}</span>
        <button @click="removeTodo(todo)">Remove</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const newTodo = ref("");
    const todos = ref([]);

    const addTodo = () => {
      if (newTodo.value.trim()) {
        todos.value.unshift({
          id: Math.random().toString(36).substring(2, 15),
          text: newTodo.value,
          done: false,
        });
        newTodo.value = "";
      }
    };

    const removeTodo = (todo) => {
      const index = todos.value.findIndex((t) => t.id === todo.id);

      todos.value.splice(index, 1);
    };

    return {
      newTodo,
      todos,
      addTodo,
      removeTodo,
    };
  },
};
</script>

<style scoped>
.todo-app {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
.todo-app > ul > li {
  display: flex;
  gap: 16px;
}
</style>
