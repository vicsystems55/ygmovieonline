<script setup>
import heroBg from '@/assets/img/33450.jpg';
import { ref } from "vue";
import logo from "@/assets/img/logo.png"; // Importing the logo

const backgroundStyle = {
  backgroundImage: `url(${heroBg})`,
  backgroundSize: 'cover',
  backgroundPosition: 'center center',
};

// Reactive state for the mobile menu
const isMenuOpen = ref(false);

// Function to toggle the menu
const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};
</script>

<template>
  <div class="home">
    <nav class="fixed w-full bg-black shadow-lg p-4 z-20 text-white">
    <div class="container mx-auto flex justify-between items-center">
      <!-- Logo -->
      <div class="flex items-center space-x-3">
        <img :src="logo" alt="YG Logo" class="h-10" />
        <h1 class="text-lg font-bold text-gold">YG Movie Productions</h1>
      </div>

      <!-- Desktop Menu -->
      <div class="hidden md:flex space-x-6">
        <a href="#hero" class="hover:text-gold">Home</a>
        <a href="#about" class="hover:text-gold">About Us</a>
        <a href="#works" class="hover:text-gold">Our Works</a>
        <a href="#join" class="hover:text-gold">Get Started</a>
      </div>

      <!-- Mobile Menu Button -->
      <div class="md:hidden">
        <button @click="toggleMenu" class="text-gold">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6h16M4 12h16M4 18h16"
            ></path>
          </svg>
        </button>
      </div>
    </div>

    <!-- Mobile Menu -->
    <div v-if="isMenuOpen" class="fixed top-0 left-0 w-full h-full bg-black/80 z-30">
      <div class="bg-black w-3/4 h-full p-6 relative">
        <button @click="toggleMenu" class="text-gold absolute top-4 right-4">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M6 18L18 6M6 6l12 12"
            ></path>
          </svg>
        </button>
        <ul class="flex flex-col space-y-4 mt-12">
          <li><a href="#hero" class="text-white hover:text-gold" @click="toggleMenu">Home</a></li>
          <li><a href="#about" class="text-white hover:text-gold" @click="toggleMenu">About Us</a></li>
          <li><a href="#works" class="text-white hover:text-gold" @click="toggleMenu">Our Works</a></li>
          <li><a href="#join" class="text-white hover:text-gold" @click="toggleMenu">Get Started</a></li>
        </ul>
      </div>
    </div>
  </nav>



<section id="hero" class="h-screen flex items-center justify-center text-center relative"
     :style="backgroundStyle"
    >
    <div class="absolute inset-0 bg-gradient-to-b from-black/90 to-black/50"></div>
    <div class="relative z-10 px-4">
        <h2 class="text-5xl sm:text-8xl font-bold text-gold/90 drop-shadow-lg leading-tight text-white">Join the Future of Filmmaking</h2>
        <div class="max-w-xl mx-auto">
            <p class="mt-5 py-5 text-white/90 drop-shadow-md text-base sm:text-xl">
                Young Gold seeks passionate content creators for collaboration! Gain exposure, industry connections, and exclusive opportunities with YG Movie Productions. Partner with us and showcase your talent—sign up today!
            </p>
        </div>
        <a href="#join"
            class="mt-6 inline-block bg-orange-500 text-black px-8 py-4 font-bold rounded-lg text-base sm:text-xl hover:bg-orange-600 transition duration-300">
            Get Started
        </a>
    </div>
</section>


    <section id="about" class="py-20 px-6 bg-black">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center">
            <div class="md:w-1/2 p-6">
                <img src="../assets/img/about.jpg" alt="About Us Image" class="rounded-lg shadow-lg">
            </div>

            <div class="md:w-1/2 p-6 text-left text-white">
                <h3 class="text-3xl font-bold">Who We Are</h3>
                <p class="mt-4">YG Movie Productions focuses on movie production, talent development, and creative
                    storytelling.</p>

                <h4 class="mt-8 text-2xl font-bold">Mission</h4>
                <p class="mt-2">YG Movie Productions is committed to entertaining, inspiring, and sparking intellectual
                    discourse by creating a deep understanding of the human condition across cultures through the
                    powerful medium of cinematic storytelling.</p>

                <h4 class="mt-8 text-2xl font-bold">Vision</h4>
                <p class="mt-2">To serve as a mirror reflecting the rich tapestry of cultural diversity across the
                    global society. We envision a future where the stories brought to life on the silver screen emanate
                    from the authentic voices of storytellers from all backgrounds.</p>

                <h4 class="mt-8 text-2xl font-bold">Commitment</h4>
                <p class="mt-2">We encourage young and upcoming talents who are passionate about making a positive
                    influence in society and driven to take Nollywood to the next level.</p>


            </div>
        </div>
        <div class="max-w-4xl mx-auto mt-8 text-center">
            <h4 class="text-2xl font-bold text-white py-5">Our Standards</h4>
            <div class="mt-2 flex flex-wrap justify-center space-x-4 md:space-x-8">
                <div class="px-4 py-2 bg-orange-500 rounded-md text-white font-bold text-xl m-2">Talent</div>
                <div class="px-4 py-2 bg-orange-500 rounded-md text-white font-bold text-xl m-2">Integrity</div>
                <div class="px-4 py-2 bg-orange-500 rounded-md text-white font-bold text-xl m-2">Passion</div>
                <div class="px-4 py-2 bg-orange-500 rounded-md text-white font-bold text-xl m-2">Unbiased</div>
                <div class="px-4 py-2 bg-orange-500 rounded-md text-white font-bold text-xl m-2">Realistic</div>
            </div>
        </div>

    </section>

    <section id="join" class="py-20 px-6 bg-gold text-black">
        <div class="max-w-2xl mx-auto text-center">
            <h3 class="text-3xl font-bold">Join Us Now</h3>
            <form class="mt-8 space-y-4" @submit.prevent="submitForm">
      <div>
        <label for="fullName" class="block text-left font-medium">Full Name <span class="text-red-500">*</span></label>
        <input type="text" id="fullName" v-model="formData.fullName" placeholder="Full Name" class="w-full p-3 border rounded mt-1" required>
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

      <div>
        <label for="file" class="block text-left font-medium">File Upload</label>
        <input type="file" id="file" ref="file" class="w-full p-3 border rounded">
      </div>

      <button type="submit" :disabled="isLoading" class="w-full bg-black text-white py-3 font-bold rounded">
        <span v-if="isLoading">Please Wait...</span>
        <span v-else>Submit</span>
      </button>
    </form>
        </div>
    </section>

    <!-- Our Works Section -->
    <section id="works" class="py-20 px-6 bg-dark">
        <div class="max-w-4xl mx-auto ">
            <h3 class="text-3xl font-bold text-gold text-center">Our Works</h3>
            <div class="mt-8 grid grid-cols-1 md:grid-cols-2 gap-6">
                <div>
                    <a href="https://www.youtube.com/watch?v=RaD0MAxMZRU">
                        <img src="../assets/img/cover1.png" class="w-full rounded">
                        <p class="mt-2">THE PA</p>
                    </a>
                </div>
                <div>
                    <a href="https://www.youtube.com/watch?v=Vbd6GU7u0gI">
                        <img src="../assets/img/cover2.png" class="w-full rounded">
                        <p class="mt-2">LETHAL AFFECTION</p>
                    </a>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-black text-center py-8">
        <div class="text-white">
            <h3 class="text-xl font-bold text-gold">YG Movie Productions</h3>
            <p class="mt-2">Contact: info@ygmovies.erp-55.com | Phone: +123456789</p>
            <div class="mt-4 space-x-4">
                <a href="https://www.facebook.com/profile.php?id=61559220190668" class="text-gold"><i class="fab fa-facebook"></i></a>
                <a href="https://www.instagram.com/younggold_mp/" class="text-gold"><i class="fab fa-instagram"></i></a>
                <a href="https://www.youtube.com/@YOUNGGOLDMOVIEPRODUCTION" class="text-gold"><i class="fab fa-youtube"></i></a>
            </div>
        </div>
    </footer>

  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      isLoading: false,
      formData: {
        fullName: '',
        email: '',
        phone: '',
        address: '',
        facebook: '',
        instagram: '',
        tiktok: '',
        twitter: '',
        other: '',
      },
    };
  },
  methods: {
    async submitForm() {
      this.isLoading = true;

      try {
        const formData = new FormData(); // Create a FormData object
        for (const key in this.formData) {
          formData.append(key, this.formData[key]); // Append form data
        }

        // Handle file upload separately
        const fileInput = this.$refs.file;
        if (fileInput.files.length > 0) {
          formData.append('file', fileInput.files[0]);
        }


        const response = await axios.post(process.env.VUE_APP_URL+'/api/yg-membership-submission', formData, {
          headers: {
            'Content-Type': 'multipart/form-data', // Important for file uploads
          },
        });

        console.log('Success:', response.data);
        alert('Membership application submitted successfully!');

        // Reset form data (except file input)
        for (const key in this.formData) {
          this.formData[key] = '';
        }
        fileInput.value = ''; // Clear the file input

      } catch (error) {
        console.error('Error:', error);
        alert('There was an error submitting your application. Please try again.');
      } finally {
        this.isLoading = false;
      }
    },
  },
};
</script>
