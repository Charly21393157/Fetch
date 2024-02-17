<template>
    <div class="user-crud">
      <h2>User CRUD</h2>
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Email</th>
            <th>Password</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id">
            <td>{{ user.id }}</td>
            <td>{{ user.email }}</td>
            <td>{{ user.password }}</td>
            <td>
              <button @click="editUser(user)">Edit</button>
              <button @click="deleteUser(user.id)">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
      <button @click="logout">Logout</button>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  import type { IUser } from '@/interfaces/IUser';
  import { userData } from '@/data/UserData';
  
  const users = ref(userData);
  const loggedIn = ref(true);
  
  const editUser = (user: IUser) => {
    const index = users.value.findIndex(u => u.id === user.id);
    if (index !== -1) {
      const newEmail = prompt('Enter new email', user.email);
      const newPassword = prompt('Enter new password', user.password);
  
      if (newEmail !== null && newPassword !== null && newEmail.trim() !== '' && newPassword.trim() !== '') {
        users.value[index].email = newEmail;
        users.value[index].password = newPassword;
        alert('User updated successfully');
      } else {
        alert('Invalid input. User not updated.');
      }
    } else {
      alert('User not found');
    }
  };
  
  
  const deleteUser = (userId: number) => {
    const index = users.value.findIndex(user => user.id === userId);
    if (index !== -1) {
      users.value.splice(index, 1);
    }
  };
  
  const logout = () => {
    loggedIn.value = false;
  };
  
  </script>
  
  <style scoped>
  .user-crud {
    text-align: center;
    margin-top: 50px;
  }
  
  table {
    width: 100%;
    border-collapse: collapse;
    background-color: white; 
  }
  
  th, td {
    border: 1px solid #ddd;
    padding: 8px;
    color: black;
  }
  
  th {
    background-color: #f2f2f2;
  }
  
  tr:nth-child(even) {
    background-color: #f2f2f2;
  }
  </style>
  