


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
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
              stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
            </svg>
          </button>
        </div>
      </div>

      <!-- Mobile Menu -->
      <div v-if="isMenuOpen" class="fixed top-0 left-0 w-full h-full bg-black/80 z-30">
        <div class="bg-black w-3/4 h-full p-6 relative">
          <button @click="toggleMenu" class="text-gold absolute top-4 right-4">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
              stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
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



    <section id="hero" class="h-screen flex items-center justify-center text-center relative" :style="backgroundStyle">
      <div class="absolute inset-0 bg-gradient-to-b from-black/90 to-black/50"></div>
      <div class="relative z-10 px-4">
        <h2 class="text-5xl sm:text-8xl font-bold text-gold/90 drop-shadow-lg leading-tight text-white">Join the Future
          of Filmmaking</h2>
        <div class="max-w-xl mx-auto">
          <p class="mt-5 py-5 text-white/90 drop-shadow-md text-base sm:text-xl">
            Young Gold seeks passionate content creators for collaboration! Gain exposure, industry connections, and
            exclusive opportunities with YG Movie Productions. Partner with us and showcase your talent—sign up today!
          </p>
        </div>
        <a href="#join"
          class="mt-6 inline-block bg-orange-500 text-black px-8 py-4 font-bold rounded-lg text-base sm:text-xl hover:bg-orange-600 transition duration-300">
          Get Started
        </a>
      </div>
    </section>
    <!-- New Movie Section -->
<section id="new-movie" class="relative py-20 bg-black text-white">
  <!-- Background image (switches for desktop/mobile) -->
  <div 
    class="absolute inset-0 bg-contain bg-center"
    :style="{
      backgroundImage: `url(${require('@/assets/img/babarajohnson.jpg')})`
    }"
  >
    <div class="absolute inset-0 bg-black/70"></div>
  </div>

  <!-- Mobile-specific background -->
  <div 
    class="absolute inset-0 bg-contain bg-no-repeat bg-center md:hidden"
    :style="{
      backgroundImage: `url(${require('@/assets/img/babarajohnson_mobile.png')})`
    }"
  >
    <div class="absolute inset-0 bg-black/70"></div>
  </div>

  <div class="relative z-10 max-w-5xl mx-auto text-center px-6">
    <h2 class="text-4xl sm:text-6xl font-bold text-gold drop-shadow-lg">Showing On Uche Jombo Tv</h2>
    <h3 class="mt-4 text-2xl sm:text-4xl font-bold">Babara Johnson</h3>
    <p class="mt-6 max-w-2xl mx-auto text-white/90 text-lg">
      A groundbreaking story from YG Movie Productions. Stay tuned for the premiere of our latest film — 
      <span class="font-semibold">Babara Johnson</span>.
    </p>
    <a href="https://www.youtube.com/watch?v=W6Oz9-hG9Ik"
      class="mt-8 inline-block bg-orange-500 text-black px-8 py-4 font-bold rounded-lg text-base sm:text-xl hover:bg-orange-600 transition duration-300">
      WATCH NOW
    </a>
  </div>
</section>


<!-- Actors Slider Section -->
<section id="cast" class="py-20 bg-black text-white relative">
  <div class="max-w-7xl mx-auto px-6">
    <h2 class="text-3xl sm:text-5xl font-bold text-center text-gold mb-10">Meet the Cast</h2>

 <swiper
  :modules="[Autoplay]"
  :slides-per-view="1.2"
  :space-between="20"
  :breakpoints="{
    768: { slidesPerView: 3, spaceBetween: 30 }
  }"
  :centered-slides="true"
  :loop="true"
  :autoplay="{
    delay: 2500,
    disableOnInteraction: false
  }"
  class="pb-12"
>
  <swiper-slide
    v-for="(poster, index) in castImages"
    :key="index"
    class="flex justify-center"
  >
    <img
      :src="poster"
      :alt="`Cast Poster ${index + 1}`"
      class="rounded-2xl shadow-2xl w-full max-w-[400px] object-cover"
    />
  </swiper-slide>
</swiper>

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

    <!-- JOIN SECTION (new) -->
    <section id="join" class="py-20 px-6 bg-gold text-black">
      <div class="max-w-4xl mx-auto flex flex-col md:flex-row items-center gap-8">
        <div class="md:w-1/2 flex justify-center">
          <img src="../assets/img/about.jpg" alt="Join Us" class="rounded-2xl shadow-2xl w-full max-w-md">
        </div>
        <div class="md:w-1/2 text-left">
          <h3 class="text-3xl font-bold mb-4">Join Us Now</h3>
          <p class="mb-6 text-lg">
            Young Gold Movie Production is on a mission to discover and empower creative talents. We're looking for passionate individuals in acting, video editing, graphics, and more — all committed to making a positive impact. Ready to grow with us? Let's create something great together.
          </p>
          <router-link to="/application" class="inline-block bg-black text-white px-8 py-4 font-bold rounded-lg text-base sm:text-xl hover:bg-orange-600 transition duration-300">
            Apply Now
          </router-link>
        </div>
      </div>
    </section>

<!-- Our Works Section -->
<section id="works" class="py-28 px-8 bg-black relative">
  <div class="max-w-6xl mx-auto text-center">
    <h3 class="text-4xl sm:text-5xl font-bold text-white mb-14">Our Works</h3>

    <Swiper
      :modules="[Autoplay]"
      :slides-per-view="1.2"
      :space-between="30"
      :loop="true"
      :centered-slides="true"
      :autoplay="{ delay: 2500, disableOnInteraction: false }"
      :breakpoints="{
        768: { slidesPerView: 2, spaceBetween: 40 },
        1024: { slidesPerView: 3, spaceBetween: 50 }
      }"
      class="pb-16"
    >
      <SwiperSlide>
        <a href="https://www.youtube.com/watch?v=RaD0MAxMZRU" class="block">
          <img 
            src="../assets/img/cover1.png" 
            class="w-full max-w-[450px] mx-auto rounded-2xl shadow-[0_0_40px_#f97316]" 
            alt="THE PA"
          >
          <p class="mt-6 text-lg text-white font-semibold">THE PA</p>
        </a>
      </SwiperSlide>

      <SwiperSlide>
        <a href="https://www.youtube.com/watch?v=Vbd6GU7u0gI" class="block">
          <img 
            src="../assets/img/cover2.png" 
            class="w-full max-w-[450px] mx-auto rounded-2xl shadow-[0_0_40px_#f97316]" 
            alt="LETHAL AFFECTION"
          >
          <p class="mt-6 text-lg text-white font-semibold">LETHAL AFFECTION</p>
        </a>
      </SwiperSlide>

      <SwiperSlide>
        <a href="https://www.youtube.com/watch?v=W6Oz9-hG9Ik" class="block">
          <img 
            src="../assets/img/babarajohnson.jpg" 
            class="w-full max-w-[450px] mx-auto rounded-2xl shadow-[0_0_40px_#f97316]" 
            alt="Babara Johnson"
          >
          <p class="mt-6 text-lg text-white font-semibold">BABARA JOHNSON</p>
        </a>
      </SwiperSlide>

            <SwiperSlide>
        <a href="https://www.youtube.com/watch?v=RaD0MAxMZRU" class="block">
          <img 
            src="../assets/img/cover1.png" 
            class="w-full max-w-[450px] mx-auto rounded-2xl shadow-[0_0_40px_#f97316]" 
            alt="THE PA"
          >
          <p class="mt-6 text-lg text-white font-semibold">THE PA</p>
        </a>
      </SwiperSlide>

      <SwiperSlide>
        <a href="https://www.youtube.com/watch?v=Vbd6GU7u0gI" class="block">
          <img 
            src="../assets/img/cover2.png" 
            class="w-full max-w-[450px] mx-auto rounded-2xl shadow-[0_0_40px_#f97316]" 
            alt="LETHAL AFFECTION"
          >
          <p class="mt-6 text-lg text-white font-semibold">LETHAL AFFECTION</p>
        </a>
      </SwiperSlide>

      <SwiperSlide>
        <a href="https://www.youtube.com/watch?v=W6Oz9-hG9Ik" class="block">
          <img 
            src="../assets/img/babarajohnson.jpg" 
            class="w-full max-w-[450px] mx-auto rounded-2xl shadow-[0_0_40px_#f97316]" 
            alt="Babara Johnson"
          >
          <p class="mt-6 text-lg text-white font-semibold">BABARA JOHNSON</p>
        </a>
      </SwiperSlide>
    </Swiper>
  </div>
</section>



<hr>

<!-- Footer -->
<footer class="bg-black text-white pt-16 pb-8">
  <div class="max-w-7xl mx-auto px-6 grid grid-cols-1 md:grid-cols-3 gap-12 text-left">

    <!-- Column 1: Logo & About -->
    <div>
      <div class="flex items-center space-x-3 mb-4">
        <img src="../assets/img/logo.png" alt="YG Logo" class="h-12">
        <h3 class="text-2xl font-bold text-gold">YG Movie Productions</h3>
      </div>
      <p class="text-gray-300">
        YG Movie Productions is committed to storytelling, talent development, and creative filmmaking that inspires audiences worldwide.
      </p>
    </div>

    <!-- Column 2: Important Links -->
    <div>
      <h4 class="text-xl font-semibold text-gold mb-4">Important Links</h4>
      <ul class="space-y-2">
        <li><a href="#hero" class="hover:text-orange-500 transition">Home</a></li>
        <li><a href="#about" class="hover:text-orange-500 transition">About Us</a></li>
        <li><a href="#works" class="hover:text-orange-500 transition">Our Works</a></li>
        <li><a href="#join" class="hover:text-orange-500 transition">Join Us</a></li>
      </ul>
    </div>

    <!-- Column 3: Social Media & Newsletter -->
    <div>
      <h4 class="text-xl font-semibold text-gold mb-4">Stay Connected</h4>
      <div class="flex space-x-4 mb-6">
        <a href="https://www.facebook.com/profile.php?id=61559220190668" class="text-gold text-2xl hover:text-orange-500"><i class="fab fa-facebook"></i></a>
        <a href="https://www.instagram.com/younggold_mp/" class="text-gold text-2xl hover:text-orange-500"><i class="fab fa-instagram"></i></a>
        <a href="https://www.youtube.com/@YOUNGGOLDMOVIEPRODUCTION" class="text-gold text-2xl hover:text-orange-500"><i class="fab fa-youtube"></i></a>
      </div>

      <form class="flex flex-col sm:flex-row gap-3">
        <input 
          type="email" 
          placeholder="Enter your email" 
          class="px-4 py-3 rounded-lg text-black w-full sm:flex-1 focus:outline-none"
        >
        <button 
          type="submit" 
          class="bg-orange-500 hover:bg-orange-600 text-black font-bold px-6 py-3 rounded-lg"
        >
          Subscribe
        </button>
      </form>
    </div>
  </div>

  <!-- Bottom Line -->
  <div class="border-t border-gray-700 mt-12 pt-6 text-center text-sm text-gray-400">
    Developed by 
    <a href="https://vicsystems.us" target="_blank" class="text-gold hover:text-orange-500 font-semibold">
      Vicsystems Technologies Ltd.
    </a>
  </div>
</footer>

<!-- WhatsApp Sticky Button -->
<a 
  href="https://wa.me/2348037835670?text=Hello%2C%20I%20will%20like%20to%20learn%20more%20about%20your%20company" 
  target="_blank"
  class="fixed bottom-6 right-6 bg-green-500 hover:bg-green-600 text-white rounded-full shadow-lg p-4 z-50 transition transform hover:scale-110"
  aria-label="Chat on WhatsApp"
>
  <i class="fab fa-whatsapp text-3xl"></i>
</a>


    <button class="d-none" @click="submitForm"></button>


    <!-- New Movie Alert Modal -->
<div v-if="showModal" class="fixed inset-0 bg-black/80 z-50 flex items-center justify-center p-4">
  <div class="bg-black rounded-xl shadow-lg w-full max-w-2xl relative overflow-hidden">
    <button @click="closeModal" class="absolute top-4 right-4 text-white hover:text-red-500 text-2xl font-bold z-10">&times;</button>
    <div class="p-6 text-center">
      <h2 class="text-2xl font-bold mb-4 text-white">🎬 New Movie Alert</h2>
      <div class="w-full" style="position: relative; padding-bottom: 56.25%; height: 0;">
       <iframe
  class="w-full h-64 md:h-96"
  src="https://www.youtube.com/embed/_BgWoaxUXmc?autoplay=1&mute=1"
  title="New Movie Alert"
  frameborder="0"
  allow="autoplay; encrypted-media"
  allowfullscreen
></iframe>

      </div>
    </div>
  </div>
</div>


  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

// Assets
import heroBg from "@/assets/img/33450.jpg";
import logo from "@/assets/img/logo.png";
import poster1 from "@/assets/img/poster (1).jpg";
import poster2 from "@/assets/img/poster (2).jpg";
import poster3 from "@/assets/img/poster (3).jpg";
import poster4 from "@/assets/img/poster (4).jpg";
import poster5 from "@/assets/img/poster (5).jpg";

// Swiper
import { Swiper, SwiperSlide } from "swiper/vue";
import { Autoplay } from "swiper/modules";
import "swiper/css";

// Register Swiper modules
// const modules = [Autoplay];

// Background styling
const backgroundStyle = {
  backgroundImage: `url(${heroBg})`,
  backgroundSize: "cover",
  backgroundPosition: "center center",
};

// State: menu
const isMenuOpen = ref(false);
const toggleMenu = () => (isMenuOpen.value = !isMenuOpen.value);

// State: modal
const showModal = ref(false);
const closeModal = () => (showModal.value = false);

// Trigger modal after delay (optional)
onMounted(() => {
  setTimeout(() => {
    // showModal.value = true;
  }, 5000);
});

// Cast posters
const castImages = [poster1, poster2, poster3, poster4, poster5];

// Form state
const isLoading = ref(false);
const formData = ref({
  full_name: "",
  email: "",
  phone: "",
  address: "",
  facebook: "",
  instagram: "",
  tiktok: "",
  twitter: "",
  other: "",
});

// Submit handler
const submitForm = async (fileInputRef) => {
  isLoading.value = true;

  try {
    const form = new FormData();
    for (const key in formData.value) {
      form.append(key, formData.value[key]);
    }

    // Handle file upload
    if (fileInputRef?.files?.length > 0) {
      form.append("file", fileInputRef.files[0]);
    }

    const response = await axios.post(
      `${import.meta.env.VITE_APP_URL}/api/yg-membership-submission`,
      form,
      {
        headers: { "Content-Type": "multipart/form-data" },
      }
    );

    console.log("Success:", response.data);
    alert("Membership application submitted successfully!");

    // Reset form
    for (const key in formData.value) {
      formData.value[key] = "";
    }
    if (fileInputRef) fileInputRef.value = "";

    return window.location.href = "/success";
  } catch (error) {
    console.error("Error:", error);
    if (error.response?.data?.errors) {
      const errors = error.response.data.errors;
      const errorMessage = Object.values(errors)
        .flat()
        .join("\n");
      alert(errorMessage);
    } else if (error.response?.data?.message) {
      alert(error.response.data.message);
    } else {
      alert("An unexpected error occurred. Please try again.");
    }
  } finally {
    isLoading.value = false;
  }
};
</script>

