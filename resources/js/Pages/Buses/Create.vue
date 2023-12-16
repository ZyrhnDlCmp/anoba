buses create


<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, router } from '@inertiajs/vue3';
import { defineProps, watchEffect, reactive } from 'vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';

const form = reactive({
    code: "",
    capacity: "",
    type: ""
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
    router.post(route("bus.store"), form);
}
</script>

<template>
    <Head title="Create Bus" />
    <AuthenticatedLayout>
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="overflow-hidden ma-8 w-100 bg-gray-100 rounded-lg border shadow-sm">
                    <div class="flex md:items-center m-6">
                        <form class="w-full max-w-sm" @submit.prevent="submit">
                            <InputLabel for="code" value="Code"/>
                            <TextInput id="code" placeholder="ABC-123" pattern="[A-Z]{3}-[0-9]{3}" title="Please enter a code in the format: ABC-123" type="text" v-model="form.code" required class="mb-4"/>

                            <InputLabel for="type" value="Select Bus Type:" class="mb-2"/>
                            <select id="type" v-model="form.type" class="mb-4 block w-full px-4 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:ring focus:ring-indigo-200 focus:outline-none focus:border-indigo-500">
                                <option value="deluxe">Deluxe</option>
                                <option value="firstclass">First Class</option>
                                <option value="luxury">Luxury</option>
                                <option value="superdeluxe">Super Deluxe</option>
                            </select>

                            <InputLabel for="capacity" value="Capacity" class="mb-2"/>
                            <TextInput id="capacity" type="number" min="25" placeholder="25-90" max="90" v-model="form.capacity" required class="mb-4"/>

                            <PrimaryButton type="submit" class="mt-4">Submit</PrimaryButton>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>