
<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, router } from '@inertiajs/vue3';
import { defineProps, reactive, computed } from 'vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';

const props = defineProps({
    busroute: Object,
    locations: Object
});

const form = reactive({
    origin: props.busroute.origin,
    destination: props.busroute.destination,
});

const existingRoute = computed(() => {
    return props.locations.find(route => route.origin === form.origin && route.destination === form.destination);
});

function update() {
    if (existingRoute.value) {
        alert('This route already exists.');
    } else if (form.origin !== form.destination) {
        router.post(`/busroute/${props.busroute.id}`, {
            _method: 'put',
            origin: form.origin,
            destination: form.destination,
        });
    } else {
        alert('Origin and destination cannot be the same');
    }
}
</script>

<template>
    <Head title="Update Bus Route" />
    <AuthenticatedLayout>
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-gray-100 overflow-hidden ma-8 rounded-lg border shadow-sm">
                    <div class="m-8">
                        <form @submit.prevent="update">
                            <InputLabel for="origin" value="Select Origin:" />
                            <select id="origin" v-model="form.origin" class="mt-1 block w-full px-4 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:ring focus:ring-indigo-200 focus:outline-none focus:border-indigo-500">
                                <option v-for="location in locations" :value="location.location">{{ location.location }}</option>
                            </select>
                            <InputLabel for="destination" value="Select Destination:" class="mt-4" />
                            <select id="destination" v-model="form.destination" class="mt-1 block w-full px-4 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:ring focus:ring-indigo-200 focus:outline-none focus:border-indigo-500">
                                <option v-for="location in locations" :value="location.location">{{ location.location }}</option>
                            </select>
                            <div class="mt-6 flex justify-center">
                                <PrimaryButton class="flex items-center bg-trymain hover:bg-trysecond text-white font-semibold px-3 py-2 rounded">
                                    <span class="ml-2">Update</span>
                                </PrimaryButton>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>