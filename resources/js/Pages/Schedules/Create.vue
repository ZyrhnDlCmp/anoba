
<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, router } from '@inertiajs/vue3';
import PrimaryButton from '@/Components/PrimaryButton.vue'
import { reactive } from 'vue'
import InputLabel from '@/Components/InputLabel.vue'
import TextInput from '@/Components/TextInput.vue'

defineProps({
    routes: Object,
    buses: Object
})

const form = reactive({
    departure_time: "",
    arrival_time: "",
    price: "",
    bus_id: "",
    route_id: ""
})

function submit() {
    router.post(route("schedule.store"), form);
}
</script>

<template>
    <Head title="Create Schedule" />
    <AuthenticatedLayout>
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-gray-100 overflow-hidden ma-8 w-100 rounded-lg border shadow-sm">
                    <div class="m-6">
                        <form class="w-full max-w-sm" @submit.prevent="submit">
                            <div>
                                <InputLabel for="departure_time" value="Departure Time" />
                                <TextInput id="departure_time" type="datetime-local" v-model="form.departure_time" required />
                            </div>

                            <div class="mt-4">
                                <InputLabel for="arrival_time" value="Arrival Time" />
                                <TextInput id="arrival_time" type="datetime-local" v-model="form.arrival_time" required />
                            </div>

                            <div class="mt-4">
                                <InputLabel for="price" value="Price" />
                                <TextInput id="price" type="number" v-model="form.price" required />
                            </div>

                            <div class="mt-4">
                                <InputLabel for="route" value="Select Bus Route:" />
                                <select id="route" v-model="form.route_id" class="block w-full px-4 py-2 mt-1 bg-white border border-gray-300 rounded-md shadow-sm focus:ring focus:ring-indigo-200 focus:outline-none focus:border-indigo-500">
                                    <option v-for="route in routes" :value="route.id">{{ route.origin }} - {{ route.destination }}</option>
                                </select>
                            </div>

                            <div class="mt-4">
                                <InputLabel for="bus" value="Select Bus" />
                                <select id="bus" v-model="form.bus_id" class="block w-full px-4 py-2 mt-1 bg-white border border-gray-300 rounded-md shadow-sm focus:ring focus:ring-indigo-200 focus:outline-none focus:border-indigo-500">
                                    <option v-for="bus in buses" :value="bus.id">{{ bus.code }} - {{ bus.type }}</option>
                                </select>
                            </div>

                            <div class="mt-6 flex justify-center">
                                <PrimaryButton type="submit" class="flex items-center bg-trymain hover:bg-trysecond text-white font-semibold px-3 py-2 rounded">
                                    <span class="ml-2">Submit</span>
                                </PrimaryButton>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>