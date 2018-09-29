<template>
    <div id="app">
        <h2>All User Data</h2>
        <table>
            <thead>
            <tr>
                <td>ID</td>
                <td>Firstname</td>
                <td>Lastname</td>
                <td>Created</td>
                <td>Gender</td>
                <td>Status</td>
                <td>Role</td>
            </tr>
            </thead>
            <tbody>
              <tr v-for="(user, index) in users" :key="index">
                  <td>{{ user[0] }}</td>
                  <td>{{ user[1] }}</td>
                  <td>{{ user[2] }}</td>
                  <td>{{ user[3] }}</td>
                  <td>{{ user[4] }}</td>
                  <td>{{ user[5] }}</td>
                  <td>{{ user[6] }}</td>
              </tr>
            </tbody>
        </table>
        <br>
        <h2>One User Data</h2>
        <hr>
        <table>
            <thead>
            <tr>
                <td>ID</td>
                <td>Firstname</td>
                <td>Lastname</td>
                <td>Created</td>
                <td>Gender</td>
                <td>Status</td>
                <td>Role</td>
            </tr>
            </thead>
            <tbody>
              <tr v-for="(u, index) in user" :key="index">
                  <td>{{ u[0] }}</td>
                  <td>{{ u[1] }}</td>
                  <td>{{ u[2] }}</td>
                  <td>{{ u[3] }}</td>
                  <td>{{ u[4] }}</td>
                  <td>{{ u[5] }}</td>
                  <td>{{ u[6] }}</td>
              </tr>
            </tbody>
        </table>
        <br>
        <h2>Update User</h2>
        <table>
        <tr><td>id:</td><td><input v-model="updateUserObj.id" placeholder="ID"></td><td></td></tr>
        <tr><td>firstname:</td><td><input v-model="updateUserObj.firstname" placeholder="firstname"></td><td></td></tr>
        <tr><td>lastname:</td><td><input v-model="updateUserObj.lastname" placeholder="lastname"></td><td></td></tr>
        <tr><td>password:</td><td><input v-model="updateUserObj.password" placeholder="password"></td><td></td></tr>
        <tr><td>created_at:</td><td> <input v-model="updateUserObj.created_at" placeholder="created at date"></td><td></td></tr>
        <tr><td>gender:</td><td><input v-model="updateUserObj.gender" placeholder="gender"></td><td></td></tr>
        <tr><td>role:</td><td><input v-model="updateUserObj.roleId" placeholder="role"></td><td></td></tr>
        <tr><td><button @click="updateUser()">Update User</button></td><td></td><td></td></tr>
        </table>
        <br>
        <h2>Delete User</h2>
        <table>
        <tr><td>id:</td><td><input v-model="deleteUserObj.id" placeholder="ID"></td><td></td></tr>
        <tr><td>created_at:</td><td><input v-model="deleteUserObj.created_at" placeholder="created at date"></td><td></td></tr>
        <tr><td><button @click="deleteUser()">Delete User</button></td><td></td><td></td></tr>
        </table>
        <br>
        <h2>Add User</h2>
        <table>
        <tr><td>firstname:</td><td><input v-model="addUserObj.firstname" placeholder="firstname"></td><td></td></tr>
        <tr><td>lastname:</td><td><input v-model="addUserObj.lastname" placeholder="lastname"></td><td></td></tr>
        <tr><td>password:</td><td><input v-model="addUserObj.password" placeholder="password"></td><td></td></tr>
        <tr><td>created_at:</td><td> <input v-model="addUserObj.created_at" placeholder="created at date"></td><td></td></tr>
        <tr><td>gender:</td><td><input v-model="addUserObj.gender" placeholder="gender"></td><td></td></tr>
        <tr><td>role:</td><td><input v-model="addUserObj.roleId" placeholder="role"></td><td></td></tr>
        <tr><td><button @click="addUser()">Add User</button></td><td></td><td></td></tr>
        </table>
        
    </div>
</template>

<script>
    export default{
      data(){
            return {
                users: [],
                user: [],
                updateUserObj: {
                    id: '',
                    firstname: '',
                    lastname: '',
                    password: '',
                    created_at: "",
                    gender: '',
                    status: true,
                    roleId: ''
                },
                deleteUserObj: {
                    id: '',
                    firstname: 'dummyOBJ',
                    lastname: 'dummyOBJ',
                    password: 'dummyOBJ',
                    created_at: "",
                    gender: 'dummyOBJ',
                    status: true,
                    roleId: '1'
                },
                addUserObj: {
                    firstname: '',
                    lastname: '',
                    password: '',
                    created_at: "",
                    gender: '',
                    status: true,
                    roleId: ''
                }
            }
        },
      created: function()
      {
        this.fetchUsers();
        this.fetchOneUser();
      },
      methods: {
        fetchUsers(){
          {
            this.$http.get('http://localhost:8084/backend/api/user/all').then((response) => {
                  this.users = response.data;
            });
          }
        },
        fetchOneUser() {
            this.$http.get('http://localhost:8084/backend/api/user/1').then((response) => {
                  this.user = response.data;
            });
        },
        updateUser() {
            fetch("http://localhost:8084/backend/api/user/" + this.updateUserObj.id, {
            body: JSON.stringify(this.updateUserObj),
            method: "PUT",
            headers: {
                "Content-Type": "application/json",
            },
        }).then(response => response.json());
        },
        deleteUser(){
            fetch("http://localhost:8084/backend/api/user/" + this.deleteUserObj.id, {
            body: JSON.stringify(this.deleteUserObj),
            method: "DELETE",
            headers: {
                "Content-Type": "application/json",
            },
        }).then(response => response.json());
        },
        addUser() {
            fetch("http://localhost:8084/backend/api/user/register", {
            body: JSON.stringify(this.addUserObj),
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
        }).then(response => response.json());
        }
    }
}
</script>