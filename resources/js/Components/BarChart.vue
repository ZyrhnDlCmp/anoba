<!-- Barchart.vue -->
<template>
  <div>
    <canvas ref="barChart"></canvas>
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from "vue";
import Chart from "chart.js/auto";

const barChart = ref(null);
const busData = ref([]);

// Declare props
const props = defineProps(["busData"]);

onMounted(() => {
  // Watch for changes in busData and update the chart
  watch(() => props.busData, (newBusData) => {
    updateChart(newBusData);
  });

  // Initial chart rendering
  updateChart(props.busData);
});

const updateChart = (data) => {
  if (!barChart.value || data.length === 0) return;

  const ctx = barChart.value.getContext("2d");

  // Destroy the existing chart instance to avoid conflicts
  if (barChart.chart) {
    barChart.chart.destroy();
  }

  // Extract labels and values from bus data
  const labels = data.map((bus) => bus.code);
  const values = data.map((bus) => bus.capacity);

  // Create a new bar chart using Chart.js
  barChart.chart = new Chart(ctx, {
    type: "bar",
    data: {
      labels: labels,
      datasets: [
        {
          label: "Seating Capacity",
          data: values,
          backgroundColor: "rgba(75, 192, 192, 0.2)",
          borderColor: "rgba(75, 192, 192, 1)",
          borderWidth: 1,
        },
      ],
    },
    options: {
      scales: {
        x: {
          type: "category",
          labels: labels,
          position: "bottom",
        },
        y: {
          beginAtZero: true,
        },
      },
    },
  });
};
</script>

<style scoped>
/* Add any additional styling for your chart if needed */
</style>