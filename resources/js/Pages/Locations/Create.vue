

<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, router } from '@inertiajs/vue3';
import { defineProps, reactive, watchEffect } from 'vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';

const form = reactive({
    location: ""
});

const props = defineProps({
    message: String
});

watchEffect(() => {
    if (props.message) {
        console.log(props.message);
        alert(props.message);
    }
});

function submit() {
    router.post(route("location.store"), form);
}
</script>

<template>
    <Head title="Create Location" />
    <AuthenticatedLayout>
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-gray-100 overflow-hidden ma-8 w-100 rounded-lg border shadow-sm">
                    <div class="m-6">
                        <form @submit.prevent="submit" class="w-full max-w-sm">
                            <div class="mb-4">
                                <InputLabel for="location" value="Location" />
                                <TextInput
                                    id="location"
                                    type="text"
                                    placeholder="Type location here"
                                    v-model="form.location"
                                    required
                                    pattern="[A-Za-z]+"
                                    title="Please enter letters only in the location field."
                                    class="mt-1 block w-full px-4 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:ring focus:ring-indigo-200 focus:outline-none focus:border-indigo-500"
                                />
                            </div>
                            <div class="mt-6">
                                <PrimaryButton class="flex items-center bg-trymain hover:bg-trysecond text-white font-semibold px-3 py-2 rounded">
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