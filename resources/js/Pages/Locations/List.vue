

<template>
    <Head title="Locations" />

    <AuthenticatedLayout>
        <div class="py-12">
            <div class="max-auto mx-auto sm:px-6 lg:px-8">
                <div class="bg-gray-100 overflow-hidden shadow-sm sm:rounded-lg px-2 py-6">
                    <div class="p-3">
                        <Link :href="route('location.create')" class="flex items-center bg-trythird hover:bg-trysecond text-white font-semibold px-3 py-2 rounded mx-2" as="button">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-5 h-5 mr-2">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M12 9v6m3-3H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z" />
                            </svg>
                            Add New Location
                        </Link>
                    </div>

                    <div class="p-6 text-gray-900">
                        <div class="overflow-x-auto w-full">
                            <table class="w-full whitespace-no-wrap">
                                <thead>
                                    <!-- <tr class="text-xs font-semibold tracking-wide text-left text-gray-500 uppercase bg-gray-50 border-b">
                        <th class="px-4 py-3">Locations</th>
                        <th class="px-4 py-3 text-right">Actions</th>
                    </tr>
                </thead>
                <tbody class="bg-white divide-y">
                    <tr v-for="location in locations" :key="location.id" class="border-b transition duration-300 ease-in-out hover:bg-neutral-300 dark:border-neutral-500 dark:hover:bg-neutral-600">
                        <td>{{ location.location }}</td>
                        <td class="flex justify-end"> -->
                           
                                    <tr class="text-xs font-semibold text-white bg-gradient-to-b from-trysecond to-trymain tracking-wide text-left text-gray-500 uppercase bg-gray-50 border-b">
                                        <th class="px-4 py-3">Locations</th>
                                        <th class="px-4 py-3">Actions</th>
                                    </tr>
                                </thead>

                                <tbody class="bg-white divide-y">
                                    <tr v-for="location in locations" :key="location.id" class="text-left border-b transition duration-300 ease-in-out hover:bg-neutral-300 dark:border-neutral-500 dark:hover:bg-neutral-600">
                                        <td class="px-4 py-3">{{ location.location }}</td>
                                        <td class="px-4 py-3 flex justify-end">
                                            <!-- Edit Button -->
                                            <Link :href="route('location.edit', { id: location.id })" class="flex items-center bg-trymain hover:bg-trysecond text-white font-semibold px-3 py-2 m-2 rounded" as="button">
                                                <!-- SVG for Edit -->
                                                <span class="ml-2">Edit Location</span>
                                            </Link>
                                            <!-- Delete Button -->
                                            <PrimaryButton title="Delete Location" class="flex items-center bg-trysecond hover:bg-trymain text-white font-semibold px-3 py-2 m-2 rounded" @Click="destroy(location.id)">
                                                <!-- SVG for Delete -->
                                                <span class="ml-2">Delete Location</span>
                                            </PrimaryButton>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>

<script setup>
import { ref } from 'vue';
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, Link, router } from '@inertiajs/vue3';
import PrimaryButton from '@/Components/PrimaryButton.vue';

defineProps({
    locations: Object
});

function destroy(id) {
    if (confirm('Are you sure you want to delete this Location?')) {
        router.delete(route("location.destroy", id));
    }
}
</script>