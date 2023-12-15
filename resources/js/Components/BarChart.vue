<template>
    <div>
      <bar-chart :data="chartData" :options="chartOptions"></bar-chart>
    </div>
  </template>
  
  <script>
  import { Bar } from 'vue-chartjs';
  
  export default {
    extends: Bar,
    props: ['data', 'options'],
    mounted() {
      this.renderChart(this.data, this.options);
    },
  };
  </script>