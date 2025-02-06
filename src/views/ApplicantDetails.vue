<template>
    <div class="max-w-3xl mx-auto p-6 bg-white shadow-md rounded-lg">
      <h2 class="text-2xl font-semibold text-gray-800 mb-4">Application Details</h2>
  
      <div v-if="loading" class="text-gray-500">Loading application details...</div>
      <div v-else-if="error" class="text-red-500">{{ error }}</div>
      <div v-else-if="applicant" class="space-y-4">
        <p><strong>Full Name:</strong> {{ applicant.full_name }}</p>
        <p><strong>Email:</strong> {{ applicant.email }}</p>
        <p><strong>Phone:</strong> {{ applicant.phone }}</p>
        <p><strong>Score:</strong> {{ applicant.score }}</p>
        <p><strong>Status:</strong> <span :class="statusClass(applicant.status)">{{ applicant.status }}</span></p>
  
        <div v-if="applicant.file_path" class="mt-4">
          <h3 class="text-lg font-medium">Submitted Video</h3>
          <video controls class="w-full rounded-lg shadow-md">
            <source :src="resolveUrl(applicant.file_path)" type="video/mp4">
            Your browser does not support the video tag.
          </video>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import { useRoute } from 'vue-router';
  import axios from 'axios';
  
  const route = useRoute();
  const applicant = ref(null);
  const loading = ref(true);
  const error = ref(null);
  
  onMounted(async () => {
    await fetchApplicantDetails(route.params.id);
  });
  
  const fetchApplicantDetails = async (id) => {
    try {
      const response = await axios.get(`${process.env.VUE_APP_URL}/api/fetch-yg-membership-details`, {
        params: { id }
      });
  
      applicant.value = response.data;
    } catch (err) {
      error.value = "Failed to load application details. Please try again.";
    } finally {
      loading.value = false;
    }
  };
  
  // ✅ Resolves the correct URL for uploaded files in Laravel's storage
  const resolveUrl = (filePath) => {
    return `${process.env.VUE_APP_URL}/storage/${filePath}`;
  };
  
  const statusClass = (status) => {
    return status === "Approved" ? "text-green-600 font-semibold" : "text-yellow-600 font-semibold";
  };
  </script>
  