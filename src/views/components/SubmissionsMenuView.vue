<template>
  <div class="p-4 sm:p-6">
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4 mb-6">
      <div class="bg-white rounded-lg shadow-md p-4 flex items-center">
        <i class="fas fa-file-alt fa-2x text-gray-500 mr-4"></i>
        <div>
          <h3 class="text-lg font-semibold">Total Submissions</h3>
          <p class="text-2xl font-bold">{{ totalSubmissions }}</p>
        </div>
      </div>
      <div class="bg-white rounded-lg shadow-md p-4 flex items-center">
        <i class="fas fa-check-circle fa-2x text-green-500 mr-4"></i>
        <div>
          <h3 class="text-lg font-semibold">Accepted Applications</h3>
          <p class="text-2xl font-bold">{{ acceptedApplications }}</p>
        </div>
      </div>
      <div class="bg-white rounded-lg shadow-md p-4 flex items-center">
        <i class="fas fa-clock fa-2x text-yellow-500 mr-4"></i>
        <div>
          <h3 class="text-lg font-semibold">Pending Review</h3>
          <p class="text-2xl font-bold">{{ pendingReview }}</p>
        </div>
      </div>
    </div>

    <div class="bg-white rounded-lg shadow-md p-4 md:p-6">
      <div class="flex flex-col md:flex-row md:justify-between md:items-center mb-4 space-y-2 md:space-y-0">
        <h2 class="text-lg font-semibold">Submissions</h2>
        <div class="flex flex-wrap gap-2">
          <button @click="sortAsc" :class="sortDirection === 'asc' ? 'bg-gray-200' : 'bg-gray-100 hover:bg-gray-300'"
            class="px-4 py-2 rounded-md transition">
            Sort Asc
          </button>
          <button @click="sortDesc" :class="sortDirection === 'desc' ? 'bg-gray-200' : 'bg-gray-100 hover:bg-gray-300'"
            class="px-4 py-2 rounded-md transition">
            Sort Desc
          </button>
        </div>
      </div>

      <div v-if="loading" class="text-center py-4">Loading submissions...</div>
      <div v-else-if="error" class="text-red-500 text-center py-4">{{ error }}</div>
      <div v-else class="overflow-x-auto">
        <div class="overflow-x-auto sm:w-full">
          <table class="w-full min-w-max">
            <thead>
              <tr class="bg-gray-100">
                <th class="px-4 py-2 text-left text-xs font-medium text-gray-500 uppercase">S/N</th>
                <th class="px-4 py-2 text-left text-xs font-medium text-gray-500 uppercase">Full Name</th>
                <th class="px-4 py-2 text-left text-xs font-medium text-gray-500 uppercase">Email</th>
                <th class="px-4 py-2 text-left text-xs font-medium text-gray-500 uppercase">Phone</th>
                <th class="px-4 py-2 text-left text-xs font-medium text-gray-500 uppercase">Score</th>
                <th class="px-4 py-2 text-left text-xs font-medium text-gray-500 uppercase">Status</th>
                <th class="px-4 py-2 text-left text-xs font-medium text-gray-500 uppercase">Action</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(submission, index) in sortedSubmissions" :key="submission.id"
                class="border-b border-gray-200 hover:bg-gray-50">
                <td class="px-4 py-2 whitespace-nowrap">{{ index + 1 }}</td>
                <td class="px-4 py-2 whitespace-nowrap">{{ submission.full_name }}</td>
                <td class="px-4 py-2 whitespace-nowrap">{{ submission.email }}</td>
                <td class="px-4 py-2 whitespace-nowrap">{{ submission.phone }}</td>
                <td class="px-4 py-2 whitespace-nowrap">{{ submission.score }}</td>
                <td class="px-4 py-2 whitespace-nowrap">
                  <span :class="statusClass(submission.status)">{{ submission.status }}</span>
                </td>
                <td class="px-4 py-2 whitespace-nowrap">
                  <button @click="goToDetails(submission.id)"
                    class="px-3 py-1 bg-blue-500 text-white rounded hover:bg-blue-600 transition">
                    View Details
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>

      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
import axios from "axios";
import { useRouter } from 'vue-router';

const submissions = ref([]);
const loading = ref(true);
const error = ref(null);
const sortDirection = ref(null);

const router = useRouter();

const fetchSubmissions = async () => {
  try {
    const response = await axios.get(`${process.env.VUE_APP_URL}/api/fetch-yg-membership-submissions`);
    submissions.value = response.data;
  } catch (err) {
    error.value = "Failed to load submissions.";
  } finally {
    loading.value = false;
  }
};



const goToDetails = (id) => {
      router.push(`/application-details/${id}`);
    };

onMounted(fetchSubmissions);

// Computed Properties
const totalSubmissions = computed(() => submissions.value.length);
const acceptedApplications = computed(() => submissions.value.filter(s => s.status === "accepted").length);
const pendingReview = computed(() => submissions.value.filter(s => s.status === "pending").length);

const sortedSubmissions = computed(() => {
  if (!sortDirection.value) return submissions.value;
  return [...submissions.value].sort((a, b) => sortDirection.value === "asc" ? a.score - b.score : b.score - a.score);
});

// Sorting Methods
const sortAsc = () => (sortDirection.value = "asc");
const sortDesc = () => (sortDirection.value = "desc");

// Status Styling
const statusClass = (status) => ({
  "px-2 py-1 rounded-md text-xs font-medium": true,
  "bg-green-100 text-green-800": status === "accepted",
  "bg-yellow-100 text-yellow-800": status === "pending",
  "bg-red-100 text-red-800": status === "rejected",
});
</script>