<template>
    <div>
      <header class="bg-white shadow-md p-4 flex justify-between items-center">
        <div class="font-bold text-xl">Dashboard</div>
        <div class="flex items-center space-x-4">
          <button class="relative">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0018 14.158V11a6.002 6.002 0 00-4-5.657V5a2 2 0 10-4 0v.343C7.67 6.165 6 8.388 6 11v3.158c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
            </svg>
            <span class="absolute top-0 right-0 inline-flex items-center justify-center px-2 py-1 text-xs font-bold leading-none text-red-100 transform translate-x-1/2 -translate-y-1/2 bg-red-600 rounded-full">3</span>
          </button>
          <div class="relative">
            <button @click="showProfileDropdown = !showProfileDropdown" class="flex items-center">
              <img src="../assets/img/logo.png" alt="Profile" class="rounded-full h-8 w-8">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd" />
              </svg>
            </button>
            <div v-if="showProfileDropdown" class="absolute right-0 mt-2 w-48 bg-white rounded-md shadow-lg">
              <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100">Log Out</a>
            </div>
          </div>
        </div>
      </header>
  
      <div class="flex h-screen">
        <aside class="w-64 bg-gray-200 p-4 hidden md:block" id="sidebar">
          <ul class="space-y-2">
            <li><a href="#" @click.prevent="loadContent('home')" class="block px-4 py-2 rounded-md hover:bg-gray-300 flex items-center"><i class="fas fa-home mr-2"></i> Home</a></li>
            <li><a href="#" @click.prevent="loadContent('submissions')" class="block px-4 py-2 rounded-md hover:bg-gray-300 flex items-center"><i class="fas fa-file-alt mr-2"></i> Submissions</a></li>
            <li><a href="#" @click.prevent="loadContent('analytics')" class="block px-4 py-2 rounded-md hover:bg-gray-300 flex items-center"><i class="fas fa-chart-bar mr-2"></i> Analytics</a></li>
          </ul>
        </aside>
  
        <aside v-if="isMobileMenuOpen" class="fixed top-0 left-0 w-full h-full bg-black/80 z-50 md:hidden">
          <div class="bg-gray-200 w-3/4 h-full p-6">
            <button @click="isMobileMenuOpen = false" class="text-gray-700 absolute top-4 right-4">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
            <ul class="space-y-2 mt-12">
              <li><a href="#" @click.prevent="loadContent('home'); isMobileMenuOpen = false" class="block px-4 py-2 rounded-md hover:bg-gray-300 flex items-center"><i class="fas fa-home mr-2"></i> Home</a></li>
              <li><a href="#" @click.prevent="loadContent('submissions'); isMobileMenuOpen = false" class="block px-4 py-2 rounded-md hover:bg-gray-300 flex items-center"><i class="fas fa-file-alt mr-2"></i> Submissions</a></li>
              <li><a href="#" @click.prevent="loadContent('analytics'); isMobileMenuOpen = false" class="block px-4 py-2 rounded-md hover:bg-gray-300 flex items-center"><i class="fas fa-chart-bar mr-2"></i> Analytics</a></li>
            </ul>
          </div>
        </aside>
  
        <main class="flex-1 bg-gray-100 p-6">
          <button @click="isMobileMenuOpen = true" class="md:hidden text-gray-700 mb-4">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
          </button>
          <div class="container mx-auto">
            <component :is="currentComponent"></component>
          </div>
        </main>
      </div>
    </div>
  </template>
  
  <script>
  import { defineAsyncComponent } from 'vue';
  
  export default {
    components: {
      Home: defineAsyncComponent(() => import('./components/HomeMenuView.vue')), // Example path
      Submissions: defineAsyncComponent(() => import('./components/SubmissionsMenuView.vue')), // Example path
      Analytics: defineAsyncComponent(() => import('./components/AnalyticsMenuView.vue')), // Example path
    },
    data() {
      return {
        currentComponent: 'Home', // Default component
        showProfileDropdown: false,
        isMobileMenuOpen: false,
      };
    },
    methods: {
      loadContent(page) {
        this.currentComponent = page.charAt(0).toUpperCase() + page.slice(1); // Dynamically set component
      },
    },
  };
  </script>