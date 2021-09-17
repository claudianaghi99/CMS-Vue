<template>
  <div>
    <h1>Content Management System</h1>
  </div>
  <button
    type="button"
    class="btn btn-primary m-2 fload-end"
    data-bs-toggle="modal"
    data-bs-target="#exampleModal"
    @click="addClick()"
  >
    Add Employee
  </button>
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
