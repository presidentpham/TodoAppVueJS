<!-- eslint-disable vue/multi-word-component-names -->
<!-- v-bind = :, v-on=@-->
<template>
  <div>
    <AddTodo @addItem="addItem" />
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @markItemCompleted="markComplete"
      @deleteItem="deleteItem"
    />
  </div>
</template>

<script>
import { ref } from "vue";
// import { v4 as uuidv4 } from "uuid";
import axios from "axios";
import TodoItem from "./TodoItem.vue";
import AddTodo from "./AddTodo.vue";
export default {
  name: "Todos-components",
  components: { TodoItem, AddTodo },
  setup() {
    const todos = ref([
      // {
      //   id: uuidv4(),
      //   title: "Work 1",
      //   completed: false,
      // },
      // {
      //   id: uuidv4(),
      //   title: "Work 2",
      //   completed: false,
      // },
      // {
      //   id: uuidv4(),
      //   title: "Work 3",
      //   completed: false,
      // },
    ]);
    const getAllTodos = async () => {
      try {
        const res = await axios.get(
          "https://jsonplaceholder.typicode.com/todos?_limit=5"
        );
        todos.value = res.data;
      } catch (error) {
        console.log(error);
      }
    };
    getAllTodos();
    const markComplete = (id) => {
      todos.value = todos.value.map((todo) => {
        if (todo.id === id) todo.completed = !todo.completed;
        return todo;
      });
    };
    const deleteItem = async (id) => {
      // todos.value = todos.value.filter((todo) => todo.id !== id);
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);
        todos.value = todos.value.filter((todo) => todo.id !== id);
      } catch (error) {
        console.log(error);
      }
    };
    const addItem = async (newTodo) => {
      //todos.value.push(newTodo);
      try {
        const res = await axios.post(
          `https://jsonplaceholder.typicode.com/todos`,
          newTodo
        );
        todos.value.unshift(res.data);
      } catch (error) {
        console.log(error);
      }
    };
    return {
      todos,
      markComplete,
      deleteItem,
      addItem,
    };
  },
};
</script>

<style>
</style>