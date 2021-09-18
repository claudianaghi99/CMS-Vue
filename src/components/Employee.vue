<template>
  <div class="all">
    <div class="table-responsive-xl">
      <table id="tabel" class="table table-bordered table-hover">
        <thead class="thead-dark">
          <tr>
            <th>
             
              Employee Id
            </th>
            <th>
              First Name
            </th>
            <th>
              Last Name
            </th>
            <th>
              Email
            </th>
            <th>
              Sex
            </th>
            <th>
              Date of Birth
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="emp in employees" v-bind:key="emp" v-bind:emp="emp">
            <td>{{ emp.EmployeeId }}</td>
            <td>{{ emp.EmployeeFirstName }}</td>
            <td>{{ emp.EmployeeLastName }}</td>
            <td>{{ emp.EmployeeEmail }}</td>
            <td>{{ emp.EmployeeSex }}</td>
            <td><span>{{moment(emp.EmployeeBirthday).format('DD MMM YYYY')}}</span></td>
            <td>
              <button
                type="button"
                class="btn btn-light mr-1"
                data-bs-toggle="modal"
                data-bs-target="#exampleModal"
                @click="editClick(emp)"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="16"
                  height="16"
                  fill="currentColor"
                  class="bi bi-pencil-square"
                  viewBox="0 0 16 16"
                >
                  <path
                    d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"
                  />
                  <path
                    fill-rule="evenodd"
                    d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z"
                  />
                </svg>
              </button>
              <button
                type="button"
                @click="deleteClick(emp.EmployeeId)"
                class="btn btn-light mr-1"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="16"
                  height="16"
                  fill="currentColor"
                  class="bi bi-trash-fill"
                  viewBox="0 0 16 16"
                >
                  <path
                    d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1H2.5zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5zM8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5zm3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0z"
                  />
                </svg>
              </button>
            </td>
          </tr>
        </tbody>
      </table>
      <div
        class="modal fade"
        id="exampleModal"
        tabindex="-1"
        aria-labelledby="exampleModalLabel"
        aria-hidden="true"
      >
        <div class="modal-dialog modal-lg modal-dialog-centered">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel">
                {{ modalTitle }}
              </h5>
              <button
                type="button"
                class="btn-close"
                data-bs-dismiss="modal"
                aria-label="Close"
              ></button>
            </div>
            <div class="modal-body">
              <div class="d-flex flex-row bd-highlight mb-3">
                <div class="p-2 w-50 bd-highlight">
                  <div class="input-group mb-3">
                    <span class="input-group-text">First Name</span>
                    <input
                      type="text"
                      class="form-control"
                      placeholder="First name"
                      onfocus="this.placeholder = ' ' "
                      onblur=" this.placeholder = 'First name'"
                      required
                      v-model="EmployeeFirstName"
                    />
                  </div>

                  <div class="input-group mb-3">
                    <span class="input-group-text">Last Name</span>
                    <input
                      type="text"
                      class="form-control"
                      placeholder="Last name"
                      onfocus="this.placeholder = ' ' "
                      onblur=" this.placeholder = 'Last name'"
                      required
                      v-model="EmployeeLastName"
                    />
                  </div>

                  <div class="input-group mb-3">
                    <span class="input-group-text">Email</span>
                    <input
                      type="text"
                      class="form-control"
                      placeholder="E-mail"
                      onfocus="this.placeholder = ' ' "
                      onblur=" this.placeholder = 'E-mail'"
                      v-model="EmployeeEmail"
                      required
                    />
                  </div>

                  <div class="input-group mb-3">
                    <span class="input-group-text">Sex</span>
                    <select
                      id="sex-list"
                      v-model="EmployeeSex"
                      class="form-control"
                      required
                    >
                      <option value="">None</option>
                      <option value="Female">Female</option>
                      <option value="Male">Male</option>
                    </select>
                  </div>

                  <div class="input-group mb-3">
                  
                    <span class="input-group-text">Date of Birth</span>
                    <input
                      type="date"
                      class="form-control"
                      v-model="EmployeeBirthday"
                      required
                    />
                  </div>
                </div>
                <div class="p-2 w-50 bd-highlight">
                  <img
                    width="250px"
                    height="250px"
                    :src="PhotoPath + PhotoFileName"
                  />
                  <input class="m-2" type="file" @change="imageUpload" />
                </div>
              </div>
              <button
                type="button"
                @click="createClick()"
                v-if="EmployeeId == 0"
                class="btn btn-dark"
              >
                Create
              </button>
              <button
                type="button"
                @click="updateClick()"
                v-if="EmployeeId != 0"
                class="btn btn-primary"
              >
                Update
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

import moment from 'moment';

const variables = {
  API_URL: "http://localhost:22612/api/",
  PHOTO_URL: "http://localhost:22612/photos/",
};
/* eslint-disable */
const emailRe = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
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

  /* eslint-disable */
  methods: {
    moment:moment,

    refreshData() {
      axios.get(variables.API_URL + "employee").then((response) => {
        this.employees = response.data;
      });
    },

    editClick(emp) {
      this.modalTitle = "Edit Employee";
      this.EmployeeId = emp.EmployeeId;
      this.EmployeeFirstName = emp.EmployeeFirstName;
      this.EmployeeLastName = emp.EmployeeLastName;
      this.EmployeeEmail = emp.EmployeeEmail;
      this.EmployeeSex = emp.EmployeeSex;
      (this.EmployeeBirthday = emp.EmployeeBirthday),
        (this.PhotoFileName = emp.PhotoFileName);
    },
    createClick() {


      this.EmployeeBirthday = moment(this.EmployeeBirthday);

      if (this.EmployeeFirstName === "") {
        alert("Enter First Name");
        return false;
      }
      if (this.EmployeeLastName === "") {
        alert("Enter Last Name");
        return false;
      }
      if (this.EmployeeEmail === "") {
        alert("Enter Email");
        return false;
      }
      if (this.EmployeeSex === "") {
        alert("Enter Sex");
        return false;
      }
      if (this.EmployeeBirthday === "") {
        alert("Enter Birthday");
        return false;
      }
      if (emailRe.test(this.EmployeeEmail)) {
      } else {
        alert("Email not valid.");
        return false;
      }

      axios
        .post(variables.API_URL + "employee", {
          EmployeeFirstName: this.EmployeeFirstName,
          EmployeeLastName: this.EmployeeLastName,
          EmployeeEmail: this.EmployeeEmail,
          EmployeeSex: this.EmployeeSex,
          EmployeeBirthday: this.EmployeeBirthday,
          PhotoFileName: this.PhotoFileName,
        })
        .then((response) => {
          this.refreshData();
          alert(response.data);
        });
    },
    updateClick() {
      axios
        .put(variables.API_URL + "employee", {
          EmployeeId: this.EmployeeId,
          EmployeeFirstName: this.EmployeeFirstName,
          EmployeeLastName: this.EmployeeLastName,
          EmployeeEmail: this.EmployeeEmail,
          EmployeeSex: this.EmployeeSex,
          EmployeeBirthday: this.EmployeeBirthday,
          PhotoFileName: this.PhotoFileName,
        })
        .then((response) => {
          this.refreshData();
          alert(response.data);
        });
    },
    deleteClick(id) {
      if (!confirm("Are you sure?")) {
        return;
      }
      axios.delete(variables.API_URL + "employee/" + id).then((response) => {
        this.refreshData();
        alert(response.data);
      });
    },
    imageUpload(event) {
      let formData = new FormData();
      formData.append("file", event.target.files[0]);
      axios
        .post(variables.API_URL + "employee/savefile", formData)
        .then((response) => {
          this.PhotoFileName = response.data;
        });
    },
  },
  mounted: function() {
    this.refreshData();
  },
};
</script>

<style>
* {
  font-family: "Nunito", sans-serif;
  margin: 0;
}

#tabel {
  background-color: rgb(230, 182, 166);
}
</style>
