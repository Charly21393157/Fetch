<template>
    <div class="register">
      <h2>Register</h2>
      <input type="email" v-model="email" placeholder="Email" />
      <input type="password" v-model="password" placeholder="Password" />
      <button @click="register">Register</button>
      <button @click="goToLogin">Login</button>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  import type { IUser } from '@/interfaces/IUser';
  import { userData } from '@/data/UserData';
  
  const email = ref('');
  const password = ref('');
  const showLogin = ref(false);
  
  const register = () => {
    const exists = userData.some(u => u.email === email.value);
    if (exists) {
      alert('User already exists');
    } else {
      const newUser: IUser = { id: userData.length + 1, email: email.value, password: password.value };
      userData.push(newUser);
      alert('Registration successful');
    }
  };
  
  const goToLogin = () => {
    showLogin.value = true;
  };
  </script>
  
  <style scoped>
  .register {
    text-align: center;
    margin-top: 50px;
  }
  </style>
  