<template>
  <div class="all">
    <div class="search-div">
      <input
        type="text"
        class="search-input"
        placeholder="Search by First Name"
        v-model="filterText"
      />
    </div>
    <div class="table-responsive-xl">
      <table id="tabel" class="table table-bordered table-hover">
        <thead class="thead-dark">
          <tr>
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
          <tr
            v-for="emp in employees"
            v-bind:key="emp"
            v-bind:emp="emp"
            @click="filteredEmployees"
          >
            <td>{{ emp.EmployeeFirstName }}</td>
            <td>{{ emp.EmployeeLastName }}</td>
            <td>{{ emp.EmployeeEmail }}</td>
            <td>{{ emp.EmployeeSex }}</td>
            <td>
              <span>{{
                moment(emp.EmployeeBirthday).format("DD MMM YYYY")
              }}</span>
            </td>
            <td class="buttons">
              <div class="edit-button">
                <button
                  type="button"
                  class="btn btn-light mr-1"
                  data-bs-toggle="modal"
                  data-bs-target="#exampleModal"
                  @click="editClick(emp)"
                >
                  <i class="fas fa-edit"></i>
                </button>
              </div>
              <div class="delete-button">
                <button
                  type="button"
                  @click="deleteClick(emp.EmployeeId)"
                  class="btn btn-light mr-1"
                >
                  <i class="fas fa-trash-alt"></i>
                </button>
              </div>
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
                class="btn btn-dark"
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

import moment from "moment";

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
      filterText: "",
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
  computed: {
    employees() {
      let filter = new RegExp(this.filterText, "i");
      return this.employees.filter((el) => el.EmployeeFirstName.match(filter));
    },
  },
  /* eslint-disable */
  methods: {
    moment: moment,

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
      this.EmployeeBirthday = emp.EmployeeBirthday;
      this.PhotoFileName = emp.PhotoFileName;
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

.buttons {
  display: flex;
  justify-content: center;
}

.edit-button {
  padding-right: 10%;
}

.edit-button i {
  padding-left: 10%;
}

.search-input {
  padding-left: 0.7%;
  width: 15%;
  border-color: black;
  border-radius: 5px;
  padding-bottom: 0.3%;
  padding-top: 0.3%;
}

.search-div {
  padding-left: 1.6%;
  padding-bottom: 1%;
}
</style>
