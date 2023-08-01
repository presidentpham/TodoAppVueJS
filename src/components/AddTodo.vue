<template>
  <form @submit="addItem">
    <input type="text" placeholder="Add work ..." v-model="title" />
    <input type="submit" value="Add" class="add-btn" />
  </form>
</template>

<script>
import { ref } from "vue";
//import { v4 as uuidv4 } from "uuid";
export default {
  name: "AddTodo",
  setup(props, context) {
    const title = ref("");
    const addItem = (event) => {
      event.preventDefault();
      const newItem = {
        //id: uuidv4(),
        title: title.value,
        completed: false,
      };
      context.emit("addItem", newItem);
      title.value = "";
    };
    return {
      title,
      addItem,
    };
  },
};
</script>

<style scoped>
form {
  display: flex;
}
input[type="text"] {
  flex: 9;
  padding: 5px;
}
input[type="submit"] {
  flex: 1;
  padding: 5px;
}
</style>