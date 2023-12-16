

<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, router } from '@inertiajs/vue3';
import { defineProps, reactive } from 'vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import InputLabel from '@/Components/InputLabel.vue';

const props = defineProps({
    location: Object
});

const form = reactive({
    location: props.location.location
});

function update() {
    router.post(`/location/${props.location.id}`, {
        _method: 'put',
        location: form.location
    });
}
</script>

<template>
    <Head title="Update Location" />
    <AuthenticatedLayout>
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-gray-100 overflow-hidden ma-8 rounded-lg border shadow-sm">
                    <div class="m-6">
                        <form @submit.prevent="update">
                            <div class="mb-4">
                                <InputLabel for="location" value="Location" />
                                <TextInput id="location" type="text" v-model="form.location" class="mt-1 block w-full px-4 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:ring focus:ring-indigo-200 focus:outline-none focus:border-indigo-500" required />
                            </div>
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