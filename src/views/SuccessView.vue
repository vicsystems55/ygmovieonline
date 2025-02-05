<template>
    <div class="relative h-screen w-full bg-cover bg-center" :style="backgroundStyle">
        <div class="absolute inset-0 bg-black bg-opacity-80"></div>

        <div class="relative flex flex-col items-center justify-center h-full text-white text-center px-4">
            <!-- Lottie Animation -->
            <Vue3Lottie :animationData="celebrationAnimation" :loop="true" :autoplay="true" class="w-60 h-60 mb-6" />

            <!-- Title & Message -->
            <h1 class="text-5xl md:text-6xl font-bold mb-6">🎉 Congratulations! 🎉</h1>
            <p class="text-xl md:text-2xl max-w-lg">
                Your Young Gold Membership submission was successful. <br />
                A confirmation email has been sent, and we will contact you soon.
            </p>
        </div>
    </div>
</template>

<script>
import Vue3Lottie from "vue3-lottie";
import celebrationAnimation from "@/assets/lottie/celebration.json"; // Place your Lottie JSON file in `src/assets/lottie/`
import heroBg from '@/assets/img/hero-bg.jpg';



export default {
    components: { Vue3Lottie },
    data() {
        return {
            celebrationAnimation,
            backgroundStyle: {
                backgroundImage: `url(${heroBg})`,
                backgroundSize: 'cover',
                backgroundPosition: 'center center',
            }
        };
    },
};
</script>