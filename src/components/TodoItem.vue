<template>
  <p :class="[todo-item, todo.completed ? 'is-completed' : '']">
    <input
      type="checkbox"
      :checked="todo.completed"
      @change="markItemCompleted"
    />
    {{ todo.title }}
    <button class="del-btn" @click="deleteItem">Delete</button>
  </p>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  setup(props, context) {
    const markItemCompleted = () => {
      context.emit("markItemCompleted", props.todo.id);
    };
    const deleteItem = () => {
      context.emit("deleteItem", props.todo.id);
    };
    return {
      markItemCompleted,
      deleteItem,
    };
  },
};
</script>

<style>
.del-btn {
  background: #ff0000;
  color: #fff;
  border: none;
  float: right;
  cursor: pointer;
  border-radius: 10px;
}
p {
  background: #f4f4f4;
  padding: 10px;
  margin: 0;
  border-bottom: 1px #ccc dotted;
}
.is-completed {
  text-decoration: line-through;
}
</style>