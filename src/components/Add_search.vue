<template>
  <div>
    <h1>Content Management System</h1>
  </div>
  <div class="button-div">
      <button
    type="button"
    class="btn btn-dark m-2"
    data-bs-toggle="modal"
    data-bs-target="#exampleModal"
    @click="addClick()"
  >
    Add Employee
  </button>
  </div>

</template>

<script>
import axios from "axios";

const variables = {
  API_URL: "http://localhost:22612/api/",
  PHOTO_URL: "http://localhost:22612/photos/",
};

export default {
  data() {
    return {
      employees: [],
      modalTitle: "",
      EmployeeId: 0,
      EmployeeFirstName: "",
      EmployeeLastName: "",
      EmployeeEmail: "",
      EmployeeSex: "",
      EmployeeBirthday: "",
      PhotoFileName: "anonymous.png",
      PhotoPath: variables.PHOTO_URL,
    };
  },
  methods: {
    refreshData() {
      axios.get(variables.API_URL + "employee").then((response) => {
        this.employees = response.data;
      });
    },
    addClick() {
      this.modalTitle = "Add Employee";
      this.EmployeeId = 0;
      this.EmployeeFirstName = "";
      this.EmployeeLastName = "";
      this.EmployeeEmail = "";
      this.EmployeeSex = "";
      (this.EmployeeBirthday = ""), (this.PhotoFileName = "anonymous.png");
    },
  },
};
</script>

<style>

/* Header */
h1 {
    display: flex;
  justify-content: center;
  padding-top: 1%;
  padding-bottom: 1%;
  color: black;
}
.button-div {
  padding-bottom:1%;
  padding-left: 1%;
}
</style>