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

/*Background*/

* {
margin: 0;
    padding:0;
    box-sizing: border-box;
    font-family: 'Nunito', sans-serif;
    
}

</style>
