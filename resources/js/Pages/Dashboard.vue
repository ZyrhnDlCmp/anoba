<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import Carousel from '@/Components/Carousel.vue';
import { Head, Link, router } from '@inertiajs/vue3';
import { watch, ref, onMounted, defineProps } from 'vue';
import {
    Chart as ChartJS,
    Title,
    Tooltip,
    Legend,
    BarElement,
    CategoryScale,
    LinearScale,
    ArcElement,
} from 'chart.js'
import { Bar, Pie } from 'vue-chartjs'

ChartJS.register(CategoryScale, ArcElement, LinearScale, BarElement, Title, Tooltip, Legend)

const props = defineProps({
    busTypes: Object,
    busCapacity: Object,
    busRoutes: Object,
});

console.log('Fetched Bus Types:', props.busRoutes);

const chartData = ref({
    labels: Object.keys(props.busRoutes),
    datasets: [
        {
        label: 'Bus Routes',
        data:  Object.values(props.busRoutes),
        backgroundColor: [
            'rgba(19, 55, 67, 1)', //lightest shade of tiffany blue
            'rgba(22, 64, 80, 1)', // other tiff blue
            'rgba(31, 89, 112, 1)', //Tiffany Blue
            'rgba(44, 65, 78, 1)',
            'rgba(26, 76, 96, 1)' //Persian Green
            
            // Add more colors as needed
        ],
        },
    ],
});

const chartData1 = ref({
    labels: Object.keys(props.busCapacity),
    datasets: [
        {
        label: 'Bus Capacity',
        data:  Object.values(props.busCapacity),
        backgroundColor: [
            'rgba(19, 55, 67, 1)', //lightest shade of tiffany blue
            'rgba(22, 64, 80, 1)', // other tiff blue
            'rgba(31, 89, 112, 1)', //Tiffany Blue
            'rgba(44, 65, 78, 1)',
            'rgba(26, 76, 96, 1)' //Persian Green
            
            // Add more colors as needed
        ],
    


        },
    ],
});
const busRouteLabels = Object.keys(props.busTypes);
const busRoutesData = Object.values(props.busTypes);

const data = {
    labels: busRouteLabels,
    
    datasets: [
        {
            label: 'Bus Type',
            data: busRoutesData,
            backgroundColor: [
            'rgba(19, 55, 67, 1)', //lightest shade of tiffany blue
            'rgba(22, 64, 80, 1)', // other tiff blue
            'rgba(31, 89, 112, 1)', //Tiffany Blue
            'rgba(44, 65, 78, 1)',
            'rgba(26, 76, 96, 1)' //Persian Green
            
            // Add more colors as needed
        ],
        },
        
    ]
}

const chartOptions = ref({
    responsive: true,
});
const options = ref({
    maintainAspectRatio: false
});
</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <div class="flex flex-col justify-center">
            <div class="p-2 px-60 dark:border-gray-700 bg-gray-200">
                <div class=" m-4 gap-4">
                    
                    <div class="flex flex-col bg-white p-6 rounded-xl">
                        <legend class="text-center font-sans">Activate Routes</legend>
                        <Bar :data="chartData" :options="chartOptions" />
                    </div>
                    <!-- <div class="grid grid-cols-2 md:grid-cols-4 gap-4 bg-white p-6 rounded-xl">
                        <Bar :data="chartData1" :options="chartOptions" />
                    </div> -->
                </div>
                <div class="flex flex-col items-center">
                    <div class="bg-white p-4 w-[500px]   rounded-xl my-5">
                        
                            <legend class="text-center  font-sans">Active buses</legend>
                            <div class="w-full md:w-auto">
                                <Pie :data="data" :options="options" />
                            </div>
                        
                    </div>
                </div>
            </div>
        </div>

    </AuthenticatedLayout>
</template>
