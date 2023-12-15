<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import BarChart from '@/Components/BarChart.vue'; // Import your BarChart component
import PieChart from '@/Components/PieChart.vue'; // Import your PieChart component
import { Head } from '@inertiajs/vue3';
import { ref } from 'vue';

const chartData = ref({
  // Define your chart data
  labels: ['Label 1', 'Label 2', 'Label 3'],
  datasets: [{
    label: 'Dataset Label',
    data: [10, 20, 30],
    backgroundColor: ['rgba(255, 99, 132, 0.2)', 'rgba(54, 162, 235, 0.2)', 'rgba(255, 206, 86, 0.2)'],
    borderColor: ['rgba(255, 99, 132, 1)', 'rgba(54, 162, 235, 1)', 'rgba(255, 206, 86, 1)'],
    borderWidth: 1,
  }],
});

const chartOptions = ref({
  // Define your chart options
  title: {
    display: true,
    text: 'My Chart Title',
  },
  legend: {
    display: true,
    position: 'top',
  },
  scales: {
    x: {
      display: true,
      title: {
        display: true,
        text: 'X Axis Title',
      },
    },
    y: {
      display: true,
      title: {
        display: true,
        text: 'Y Axis Title',
      },
    },
  },
});

</script>

<template>
  <Head title="Dashboard" />

  <AuthenticatedLayout>
    <div class="flex justify-center">
      <div class="p-6 dark:border-gray-700 mt-14 bg-blue-400">
        <div class="grid grid-cols-2 md:grid-cols-3 gap-4">
          <div>
            <!-- Insert the BarChart and PieChart components with the data and options -->
            <BarChart :data="chartData" :options="chartOptions" />
            <PieChart :data="chartData" :options="chartOptions" />
          </div>
        </div>
      </div>
    </div>
  </AuthenticatedLayout>
</template>