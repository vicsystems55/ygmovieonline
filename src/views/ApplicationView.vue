<template>
  <div class="application-page relative min-h-screen">
    <!-- Header Menu -->
    <nav class="fixed w-full bg-black shadow-lg p-4 z-20 text-white top-0 left-0">
      <div class="container mx-auto flex justify-between items-center">
        <!-- Logo -->
        <div class="flex items-center space-x-3">
          <img :src="logo" alt="YG Logo" class="h-10" />
          <h1 class="text-lg font-bold text-gold">YG Movie Productions</h1>
        </div>
        <!-- Desktop Menu -->
        <div class="hidden md:flex space-x-6">
          <router-link to="/" class="hover:text-gold">Home</router-link>
          <a href="/#about" class="hover:text-gold">About Us</a>
          <a href="/#works" class="hover:text-gold">Our Works</a>
          <router-link to="/application" class="hover:text-gold">Get Started</router-link>
        </div>
        <!-- Mobile Menu Button -->
        <div class="md:hidden">
          <button @click="toggleMenu" class="text-gold">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
            </svg>
          </button>
        </div>
      </div>
      <!-- Mobile Menu -->
      <div v-if="isMenuOpen" class="fixed top-0 left-0 w-full h-full bg-black/80 z-30">
        <div class="bg-black w-3/4 h-full p-6 relative">
          <button @click="toggleMenu" class="text-gold absolute top-4 right-4">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
            </svg>
          </button>
          <ul class="flex flex-col space-y-4 mt-12">
            <li><router-link to="/" class="text-white hover:text-gold" @click="toggleMenu">Home</router-link></li>
            <li><a href="/#about" class="text-white hover:text-gold" @click="toggleMenu">About Us</a></li>
            <li><a href="/#works" class="text-white hover:text-gold" @click="toggleMenu">Our Works</a></li>
            <li><router-link to="/application" class="text-white hover:text-gold" @click="toggleMenu">Get Started</router-link></li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- Header with background image, golden ambient light, and overlay -->
    <header class="relative h-72 flex items-center justify-center overflow-hidden mt-16">
      <div class="absolute inset-0 bg-cover bg-center" :style="headerBgStyle"></div>
      <div class="absolute inset-0 bg-black opacity-70"></div>
      <div class="relative z-10 text-center">
        <h1 class="text-4xl md:text-5xl font-bold text-white drop-shadow-lg">Join Us Now</h1>
      </div>
    </header>

    <!-- Application Form -->
    <section class="py-16 px-4 min-h-[60vh]" :style="appBgStyle">
      <div class="max-w-2xl mx-auto bg-white/90 rounded-2xl shadow-xl p-8">
        <h2 class="text-2xl font-bold mb-6 text-center text-black">Application Form</h2>
        <form class="space-y-4" @submit.prevent="submitForm">
          <!-- Position Section -->
          <div>
            <label class="block text-left font-medium mb-2">Position <span class="text-red-500">*</span></label>
            <div class="flex flex-col sm:flex-row gap-4">
              <label class="flex-1 cursor-pointer border-2 rounded-xl p-4 flex items-center gap-3 transition hover:border-gold" :class="{'border-gold ring-2 ring-gold': formData.position === 'video_editor', 'border-gray-300': formData.position !== 'video_editor'}">
                <input type="radio" name="position" value="video_editor" v-model="formData.position" class="accent-gold h-5 w-5" required>
                <span class="font-semibold">Video Editor</span>
              </label>
              <label class="flex-1 cursor-pointer border-2 rounded-xl p-4 flex items-center gap-3 transition hover:border-gold" :class="{'border-gold ring-2 ring-gold': formData.position === 'actor', 'border-gray-300': formData.position !== 'actor'}">
                <input type="radio" name="position" value="actor" v-model="formData.position" class="accent-gold h-5 w-5" required>
                <span class="font-semibold">Actor/Actress</span>
              </label>
              <label class="flex-1 cursor-pointer border-2 rounded-xl p-4 flex items-center gap-3 transition hover:border-gold" :class="{'border-gold ring-2 ring-gold': formData.position === 'writer', 'border-gray-300': formData.position !== 'writer'}">
                <input type="radio" name="position" value="writer" v-model="formData.position" class="accent-gold h-5 w-5" required>
                <span class="font-semibold">Writer</span>
              </label>
            </div>
          </div>
          <!-- File Upload -->
          <div>
            <label for="file" class="block text-left font-medium">File Upload <span class="text-red-500">*</span> (Maximum size 50MB, Maximum 5 minutes)</label>
            <input type="file" id="file" ref="file" class="w-full p-3 border rounded">
          </div>
          <div>
            <label for="fullName" class="block text-left font-medium">Full Name <span class="text-red-500">*</span></label>
            <input type="text" id="fullName" v-model="formData.full_name" placeholder="Full Name" class="w-full p-3 border rounded mt-1" required>
          </div>
          <div>
            <label for="email" class="block text-left font-medium">Email <span class="text-red-500">*</span></label>
            <input type="email" id="email" v-model="formData.email" placeholder="Email" class="w-full p-3 border rounded mt-1" required>
          </div>
          <div>
            <label for="phone" class="block text-left font-medium">Phone Number <span class="text-red-500">*</span></label>
            <input type="tel" id="phone" v-model="formData.phone" placeholder="Phone Number" class="w-full p-3 border rounded mt-1" required>
          </div>
          <div>
            <label for="address" class="block text-left font-medium">Address <span class="text-red-500">*</span></label>
            <input type="text" id="address" v-model="formData.address" placeholder="Address" class="w-full p-3 border rounded mt-1" required>
          </div>
          <div>
            <label for="facebook" class="block text-left font-medium">Facebook Profile URL</label>
            <input type="url" id="facebook" v-model="formData.facebook" placeholder="Facebook URL" class="w-full p-3 border rounded mt-1">
          </div>
          <div>
            <label for="instagram" class="block text-left font-medium">Instagram Profile URL</label>
            <input type="url" id="instagram" v-model="formData.instagram" placeholder="Instagram URL" class="w-full p-3 border rounded mt-1">
          </div>
          <div>
            <label for="tiktok" class="block text-left font-medium">TikTok Profile URL</label>
            <input type="url" id="tiktok" v-model="formData.tiktok" placeholder="TikTok URL" class="w-full p-3 border rounded mt-1">
          </div>
          <div>
            <label for="twitter" class="block text-left font-medium">Twitter Profile URL</label>
            <input type="url" id="twitter" v-model="formData.twitter" placeholder="Twitter URL" class="w-full p-3 border rounded mt-1">
          </div>
          <div>
            <label for="other" class="block text-left font-medium">Other Social Media/Portfolio Link</label>
            <input type="url" id="other" v-model="formData.other" placeholder="Other Link" class="w-full p-3 border rounded mt-1">
          </div>
          <button type="submit" :disabled="isLoading" class="w-full bg-black text-white py-3 font-bold rounded">
            <span v-if="isLoading">Please Wait...</span>
            <span v-else>Submit</span>
          </button>
        </form>
      </div>
    </section>

    <!-- Footer (copied from HomeView.vue) -->
    <footer class="bg-black text-center py-8">
      <div class="text-white">
        <h3 class="text-xl font-bold text-gold">YG Movie Productions</h3>
        <p class="mt-2">Contact: younggoldproductions@gmail.com</p>
        <div class="mt-4 space-x-4">
          <a href="https://www.facebook.com/profile.php?id=61559220190668" class="text-gold"><i class="fab fa-facebook"></i></a>
          <a href="https://www.instagram.com/younggold_mp/" class="text-gold"><i class="fab fa-instagram"></i></a>
          <a href="https://www.youtube.com/@YOUNGGOLDMOVIEPRODUCTION" class="text-gold"><i class="fab fa-youtube"></i></a>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import axios from 'axios';
import heroBg from '@/assets/img/hero-bg.jpg';
import logo from '@/assets/img/logo.png';
import applicationBg from '@/assets/img/applicationbg.jpg';

const router = useRouter();
const headerBgStyle = {
  backgroundImage: `url(${heroBg})`,
  backgroundSize: 'cover',
  backgroundPosition: 'center center',
};

const appBgStyle = {
  backgroundImage: `url(${applicationBg})`,
  backgroundSize: 'cover',
  backgroundPosition: 'center center',
};

// Menu state for mobile
const isMenuOpen = ref(false);
const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const isLoading = ref(false);
const formData = ref({
  full_name: '',
  email: '',
  phone: '',
  address: '',
  facebook: '',
  instagram: '',
  tiktok: '',
  twitter: '',
  other: '',
  position: '',
});

const submitForm = async () => {
  isLoading.value = true;
  try {
    const data = new FormData();
    for (const key in formData.value) {
      data.append(key, formData.value[key]);
    }
    // Handle file upload
    const fileInput = document.getElementById('file');
    if (fileInput && fileInput.files.length > 0) {
      data.append('file', fileInput.files[0]);
    }
    await axios.post(process.env.VUE_APP_URL + '/api/yg-membership-submission', data, {
      headers: {
        'Content-Type': 'multipart/form-data',
      },
    });
    alert('Membership application submitted successfully!');
    // Reset form
    for (const key in formData.value) {
      formData.value[key] = '';
    }
    if (fileInput) fileInput.value = '';
    router.push('/success');
  } catch (error) {
    if (error.response && error.response.data && error.response.data.errors) {
      const errors = error.response.data.errors;
      let errorMessage = '';
      for (const field in errors) {
        errors[field].forEach(message => {
          errorMessage += `${message}\n`;
        });
      }
      alert(errorMessage.trim());
    } else if (error.response && error.response.data && error.response.data.message) {
      alert(error.response.data.message);
    } else {
      alert('An unexpected error occurred. Please try again.');
    }
  } finally {
    isLoading.value = false;
  }
};
</script>

<style scoped>
.bg-gold {
  background-color: #FFD700;
}
.border-gold {
  border-color: #FFD700 !important;
}
.ring-gold {
  box-shadow: 0 0 0 2px #FFD700 !important;
}
/* No longer needed: .app-bg */
</style> 