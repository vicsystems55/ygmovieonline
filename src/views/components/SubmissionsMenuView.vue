<template>
  <div class="p-6">
    <!-- Statistics Cards -->
    <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
      <div class="card bg-white rounded-lg shadow-md p-4 flex items-center">
        <div class="mr-4"><i class="fas fa-file-alt fa-2x text-gray-500"></i></div>
        <div>
          <h3 class="text-lg font-semibold mb-2">Total Submissions</h3>
          <div class="text-2xl font-bold">{{ totalSubmissions }}</div>
        </div>
      </div>
      <div class="card bg-white rounded-lg shadow-md p-4 flex items-center">
        <div class="mr-4"><i class="fas fa-check-circle fa-2x text-green-500"></i></div>
        <div>
          <h3 class="text-lg font-semibold mb-2">Accepted Applications</h3>
          <div class="text-2xl font-bold">{{ acceptedApplications }}</div>
        </div>
      </div>
      <div class="card bg-white rounded-lg shadow-md p-4 flex items-center">
        <div class="mr-4"><i class="fas fa-clock fa-2x text-yellow-500"></i></div>
        <div>
          <h3 class="text-lg font-semibold mb-2">Pending Review</h3>
          <div class="text-2xl font-bold">{{ pendingReview }}</div>
        </div>
      </div>
    </div>

    <!-- Submissions Table -->
    <div class="card bg-white rounded-lg shadow-md p-6">
      <div class="flex justify-between items-center mb-4">
        <h2 class="text-lg font-semibold">Submissions</h2>
        <div class="flex space-x-2">
          <button @click="sortAsc" :class="{ 'bg-gray-200': sortDirection === 'asc', 'bg-gray-100 hover:bg-gray-300 px-4 py-2 rounded-md transition': true }">
            Sort Asc
          </button>
          <button @click="sortDesc" :class="{ 'bg-gray-200': sortDirection === 'desc', 'bg-gray-100 hover:bg-gray-300 px-4 py-2 rounded-md transition': true }">
            Sort Desc
          </button>
        </div>
      </div>

      <div v-if="loading" class="text-center py-4">Loading submissions...</div>
      <div v-else-if="error" class="text-red-500 text-center py-4">{{ error }}</div>
      <div v-else class="overflow-x-auto">

        <table  class="min-w-full divide-y divide-gray-200 ">
          <thead>
            <tr>
              <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">S/N</th>
              <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Full Name</th>
              <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Email</th>
              <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Phone</th>
              <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Score</th>
              <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Status</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(submission, index) in sortedSubmissions" :key="submission.id" class="border-b border-gray-200 hover:bg-gray-50">
              <td class="px-6 py-4 whitespace-nowrap">{{ index + 1 }}</td>
              <td class="px-6 py-4 whitespace-nowrap">{{ submission.full_name }}</td>
              <td class="px-6 py-4 whitespace-nowrap">{{ submission.email }}</td>
              <td class="px-6 py-4 whitespace-nowrap">{{ submission.phone }}</td>
              <td class="px-6 py-4 whitespace-nowrap">{{ submission.score }}</td>
              <td class="px-6 py-4 whitespace-nowrap">
                <span :class="statusClass(submission.status)">{{ submission.status }}</span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
import axios from "axios";

const submissions = ref([]);
const loading = ref(true);
const error = ref(null);
const sortDirection = ref(null);

const fetchSubmissions = async () => {
  try {
    const response = await axios.get(process.env.VUE_APP_URL+"/api/fetch-yg-membership-submissions");
    submissions.value = response.data;
  } catch (err) {
    error.value = "Failed to load submissions.";
  } finally {
    loading.value = false;
  }
};

onMounted(fetchSubmissions);

// Computed Properties
const totalSubmissions = computed(() => submissions.value.length);
const acceptedApplications = computed(() => submissions.value.filter(s => s.status === "accepted").length);
const pendingReview = computed(() => submissions.value.filter(s => s.status === "pending").length);

const sortedSubmissions = computed(() => {
  if (!sortDirection.value) return submissions.value;
  return [...submissions.value].sort((a, b) => {
    return sortDirection.value === "asc" ? a.score - b.score : b.score - a.score;
  });
});

// Sorting Methods
const sortAsc = () => (sortDirection.value = "asc");
const sortDesc = () => (sortDirection.value = "desc");

// Status Styling
const statusClass = (status) => {
  return {
    "px-2 py-1 rounded-md text-xs font-medium": true,
    "bg-green-100 text-green-800": status === "accepted",
    "bg-yellow-100 text-yellow-800": status === "pending",
    "bg-red-100 text-red-800": status === "rejected",
  };
};
</script>
