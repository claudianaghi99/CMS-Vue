<template>
  <Add></Add>
  <Employee></Employee>
</template>

<script>
import Employee from "./components/Employee.vue";
import Add from "./components/Add_search.vue";

export default {
  name: "App",
  components: {
    Employee,
    Add,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
