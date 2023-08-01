<template>
  <div class="app">
    <Header />
    <Todos />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Todos from "./components/Todos.vue";
export default {
  name: "app",
  components: { Header, Todos },
};
</script>
<style>
#app {
  font-family: Arial, Helvetica, sans-serif;
}
</style>