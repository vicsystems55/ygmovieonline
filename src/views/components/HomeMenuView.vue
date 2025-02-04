<template>
    <div class="p-6">
      <div class="flex justify-between items-center mb-4">
        <h2 class="text-lg font-semibold">Submissions Trend</h2>
        <select v-model="selectedView" class="p-2 border rounded-md">
          <option value="daily">Per Day (Week)</option>
          <option value="monthly">Per Month (Year)</option>
        </select>
      </div>
      <div class="card bg-white rounded-lg shadow-md p-6">  <LineChart :chart-data="chartData" :options="chartOptions" class="w-full h-96" />
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from "vue";
  import { LineChart } from "vue-chart-3";
  import { Chart, registerables } from 'chart.js';
  
  Chart.register(...registerables);
  
  const chartOptions = ref({
    responsive: true,
    maintainAspectRatio: false,
    scales: {
      x: { type: 'category' },
      y: {
        title: {
          display: true,
          text: 'Number of Submissions'
        }
      }
    },
    plugins: {
      title: {
        display: true,
        text: 'Submissions Trend',
        font: {
          size: 16
        }
      },
      // Add the shadow to the line
      datalabels: {
        // ... other datalabels options
        // You can also use the 'beforeDraw' hook to add the shadow
        // to the line, but the datalabels plugin is simpler for this
        // example.  For more complex shadows, the 'beforeDraw' hook
        // would be a better approach.
      }
    },
    tension: 0.3,
    elements: { // Add shadow to the line
      line: {
        tension: 0.3,
        borderWidth: 2,
        // The following boxShadow properties don't work directly on the line.
        // Instead, we are using the datalabels plugin to create the shadow
        // effect (see above).
      },
      point: { // You can add shadow to the points if you want
        // ... point options
      }
    }
  });
  
  
  const dailyData = ref({
    labels: ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"],
    datasets: [
      {
        label: "Submissions Per Day",
        data: [10, 20, 15, 25, 30, 18, 22],
        borderColor: "#4CC0E8",
        backgroundColor: "rgba(76, 192, 232, 0.2)",
        fill: true,
      },
    ],
  });
  
  const monthlyData = ref({
    labels: ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"],
    datasets: [
      {
        label: "Submissions Per Month",
        data: [100, 120, 150, 200, 180, 220, 250, 270, 300, 320, 350, 400],
        borderColor: "#E62947",
        backgroundColor: "rgba(230, 41, 71, 0.2)",
        fill: true,
      },
    ],
  });
  
  const selectedView = ref("daily");
  const chartData = computed(() => (selectedView.value === "daily" ? dailyData.value : monthlyData.value));
  
  </script>
  
  <style scoped>
  /* You likely don't need any styles here, as Tailwind handles it */
  </style>