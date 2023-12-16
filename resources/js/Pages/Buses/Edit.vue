bus edit

<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, router } from '@inertiajs/vue3';
import { defineProps, reactive } from 'vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import InputLabel from '@/Components/InputLabel.vue';

const props = defineProps({
    bus: Object
});

const form = reactive({
    capacity: props.bus.capacity,
    code: props.bus.code,
    type: props.bus.type
});

function update() {
    router.post(`/bus/${props.bus.id}`, {
        _method: 'put',
        capacity: form.capacity,
        code: form.code,
        type: form.type
    });
}
</script>

<template>
    <Head title="Update Bus" />
    <AuthenticatedLayout>
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-gray-100 overflow-hidden ma-8 w-100 rounded-lg border shadow-sm">
                    <div class="m-6">
                        <form @submit.prevent="update">
                            <InputLabel for="code" value="Code" />
                            <TextInput id="code" type="text" v-model="form.code" required />
                            <InputLabel for="type" class="block font-medium text-gray-700">Select Bus Type:</InputLabel>
                            <select id="type" v-model="form.type" class="mt-1 block w-full px-4 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:ring focus:ring-indigo-200 focus:outline-none focus:border-indigo-500">
                                <option value="deluxe">Deluxe</option>
                                <option value="firstclass">First Class</option>
                                <option value="luxury">Luxury</option>
                                <option value="superdeluxe">Super Deluxe</option>
                            </select>
                            <InputLabel for="capacity" value="Capacity" />
                            <TextInput id="capacity" type="number" v-model="form.capacity" required />
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