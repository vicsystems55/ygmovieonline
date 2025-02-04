<template>
    <div class="p-6">
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
      <div class="card bg-white rounded-lg shadow-md p-4 flex items-center">
        <div class="mr-4"> <i class="fas fa-file-alt fa-2x text-gray-500"></i> </div>
        <div>
          <h3 class="text-lg font-semibold mb-2">Total Submissions</h3>
          <div class="text-2xl font-bold">{{ totalSubmissions }}</div>
          <div class="text-sm" :class="{ 'text-green-500': submissionChange >= 0, 'text-red-500': submissionChange < 0 }">
            {{ submissionChange }}% <span v-if="submissionChange >= 0">▲</span><span v-else>▼</span>
          </div>
        </div>
      </div>
      <div class="card bg-white rounded-lg shadow-md p-4 flex items-center">
        <div class="mr-4"> <i class="fas fa-check-circle fa-2x text-green-500"></i> </div>
        <div>
          <h3 class="text-lg font-semibold mb-2">Accepted Applications</h3>
          <div class="text-2xl font-bold">{{ acceptedApplications }}</div>
        </div>
      </div>
      <div class="card bg-white rounded-lg shadow-md p-4 flex items-center">
        <div class="mr-4"> <i class="fas fa-clock fa-2x text-yellow-500"></i> </div>
        <div>
          <h3 class="text-lg font-semibold mb-2">Pending Review</h3>
          <div class="text-2xl font-bold">{{ pendingReview }}</div>
        </div>
      </div>
    </div>
  
      <div class="card bg-white rounded-lg shadow-md p-6 overflow-x-auto">
        <div class="flex justify-between items-center mb-4">
          <h2 class="text-lg font-semibold">Submissions</h2>
          <div class="flex space-x-2">
          <button @click="sortAsc" :class="{'bg-gray-200': sortDirection === 'asc', 'bg-gray-100 hover:bg-gray-300 px-4 py-2 rounded-md transition': true }">Sort Asc</button>
          <button @click="sortDesc" :class="{'bg-gray-200': sortDirection === 'desc', 'bg-gray-100 hover:bg-gray-300 px-4 py-2 rounded-md transition': true }">Sort Desc</button>
          </div>
        </div>
        <table class="min-w-full divide-y divide-gray-200">
          <thead>
            <tr>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">S/N</th>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Avatar</th>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Full Name</th>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Email</th>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Phone</th>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Date</th>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(submission, index) in sortedSubmissions" :key="submission.id" class="border-b border-gray-200 hover:bg-gray-50">
              <td class="px-6 py-4 whitespace-nowrap">{{ index + 1 }}</td>
              <td class="px-6 py-4 whitespace-nowrap">
                <img :src="submission.avatar" alt="Avatar" class="h-8 w-8 rounded-full">
              </td>
              <td class="px-6 py-4 whitespace-nowrap">{{ submission.fullname }}</td>
              <td class="px-6 py-4 whitespace-nowrap">{{ submission.email }}</td>
              <td class="px-6 py-4 whitespace-nowrap">{{ submission.phone }}</td>
              <td class="px-6 py-4 whitespace-nowrap">{{ submission.date }}</td>
              <td class="px-6 py-4 whitespace-nowrap">
                <span :class="[
                  'px-2 py-1 rounded-md text-xs font-medium',
                  submission.status === 'accepted' ? 'bg-green-100 text-green-800' :
                  submission.status === 'pending' ? 'bg-yellow-100 text-yellow-800' :
                  submission.status === 'rejected' ? 'bg-red-100 text-red-800' :
                  '' // Default class if status is not recognized
                ]">
                  {{ submission.status }}
                </span>
              </td>            
              <td class="px-6 py-4 whitespace-nowrap text-right">
                <button class="text-indigo-600 hover:text-indigo-900">View More</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue';
  
  const submissions = ref([
    {
      id: 1,
      avatar: 'https://via.placeholder.com/40',
      fullname: 'John Doe',
      email: 'john.doe@example.com',
      phone: '123-456-7890',
      date: '2023-10-26',
      status: 'accepted',
    },
    {
      id: 2,
      avatar: 'https://via.placeholder.com/40',
      fullname: 'Jane Smith',
      email: 'jane.smith@example.com',
      phone: '987-654-3210',
      date: '2023-10-25',
      status: 'pending',
    },
    {
      id: 3,
      avatar: 'https://via.placeholder.com/40',
      fullname: 'Peter Jones',
      email: 'peter.jones@example.com',
      phone: '555-123-4567',
      date: '2023-10-27',
      status: 'accepted',
    },
    {
      id: 4,
      avatar: 'https://via.placeholder.com/40',
      fullname: 'Alice Johnson',
      email: 'alice.johnson@example.com',
      phone: '111-222-3333',
      date: '2023-10-24',
      status: 'rejected', // Added 'rejected' status for demo
    },
    {
      id: 5,
      avatar: 'https://via.placeholder.com/40',
      fullname: 'Bob Williams',
      email: 'bob.williams@example.com',
      phone: '444-555-6666',
      date: '2023-10-28',
      status: 'pending',
    },
  ]);
  
  const totalSubmissions = computed(() => submissions.value.length);
  const acceptedApplications = computed(() => submissions.value.filter(s => s.status === 'accepted').length);
  const pendingReview = computed(() => submissions.value.filter(s => s.status === 'pending').length);
  const submissionChange = ref(0);
  
  const sortDirection = ref(null);
  
  const sortedSubmissions = computed(() => {
      if (!sortDirection.value) {
          return submissions.value;
      }
      const sorted = [...submissions.value];
      sorted.sort((a, b) => {
        const dateA = new Date(a.date);
        const dateB = new Date(b.date);
  
          if (sortDirection.value === 'asc') {
              return dateA.getTime() - dateB.getTime();
          } else {
              return dateB.getTime() - dateA.getTime();
          }
      });
      return sorted;
  });
  
  const sortAsc = () => {
    sortDirection.value = 'asc';
  };
  
  const sortDesc = () => {
    sortDirection.value = 'desc';
  };
  </script>
  
