<template>
    <div class="login">
      <h2>Login</h2>
      <input type="email" v-model="email" placeholder="Email" />
      <input type="password" v-model="password" placeholder="Password" />
      <button @click="login">Login</button>
      <button @click="goToRegister">Register</button>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  import type { IUser } from '@/interfaces/IUser';
  import { userData } from '@/data/UserData';
  
  const email = ref('');
  const password = ref('');
  const showRegister = ref(true);
  
  const login = () => {
    const user: IUser | undefined = userData.find(u => u.email === email.value && u.password === password.value);
    if (user) {
      alert('Login successful');
    } else {
      alert('Invalid email or password');
    }
  };
  
  const goToRegister = () => {
    showRegister.value = true;
  };
  </script>
  
  <style scoped>
  .login {
    text-align: center;
    margin-top: 50px;
  }
  </style>
  