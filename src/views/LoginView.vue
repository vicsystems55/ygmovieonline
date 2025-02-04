<template>
    <div class="bg-gray-900 h-screen flex items-center justify-center overflow-hidden">
      <div class="bg-gray-900 rounded-lg shadow-lg p-8 w-96 relative">
        <div class="flex justify-center mb-6">
          <img src="../assets/img/logo.png" alt="Logo" class="h-20 w-auto">
        </div>
        <h2 class="text-2xl font-semibold mb-4 text-center text-white">Login</h2>
        <form @submit.prevent="login">
          <div class="mb-4">
            <label for="email" class="block text-gray-300 text-sm font-bold mb-2">Email</label>
            <input type="email" id="email" v-model="email"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-white bg-gray-800 leading-tight focus:outline-none focus:shadow-outline"
              placeholder="Enter your email">
          </div>
          <div class="mb-6">
            <label for="password" class="block text-gray-300 text-sm font-bold mb-2">Password</label>
            <input type="password" id="password" v-model="password"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-white bg-gray-800 leading-tight focus:outline-none focus:shadow-outline"
              placeholder="Enter your password">
          </div>
          <div class="flex items-center justify-between">
            <button type="submit"
              class="bg-gradient-to-r from-yellow-500 to-orange-500 hover:from-yellow-600 hover:to-orange-600 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
              Login
            </button>
            <a href="#" class="inline-block align-baseline font-bold text-sm text-yellow-500 hover:text-yellow-600">
              Forgot Password?
            </a>
          </div>
        </form>
        <div class="absolute inset-0 pointer-events-none">
          <div class="absolute top-0 left-0 w-full h-full bg-gradient-to-r from-red-500 via-transparent to-black opacity-20"></div>
          <div class="absolute top-0 left-0 w-full h-full bg-gradient-to-r from-black via-transparent to-red-500 opacity-20"></div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  // ... (your script code - email, password, login function, etc.)
  import { ref } from 'vue';
  import { useRouter } from 'vue-router';
  
  const email = ref('');
  const password = ref('');
  const router = useRouter();
  
  const login = () => {
    // Here you would typically make an API call to authenticate the user.
    // For this example, we'll just simulate a successful login.
  
    if (email.value === 'test@example.com' && password.value === 'password') {
      // Redirect to the desired page after login (e.g., dashboard)
      console.log('Login successful');
      router.push('/dashboard'); // Replace '/dashboard' with your route
    } else {
      alert('Invalid email or password');
    }
  };
  
  </script>
  
  <style scoped>
  
  </style>