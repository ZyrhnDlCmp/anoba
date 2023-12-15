<template>
    <div>
      <pie-chart :data="chartData" :options="chartOptions"></pie-chart>
    </div>
  </template>
  
  <script>
  import { Pie } from 'vue-chartjs';
  
  export default {
    extends: Pie,
    props: ['data', 'options'],
    mounted() {
      this.renderChart(this.data, this.options);
    },
  };
  </script>