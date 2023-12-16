

<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, router } from '@inertiajs/vue3';
import { defineProps, reactive } from 'vue';
import TextInput from '@/Components/TextInput.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';

const form = reactive({
  origin: "",
  destination: "",
});

function submit() {
  if (form.origin !== form.destination) {
    router.post(route("busroutes.store"), form);
  } else {
    alert("Origin and destination cannot be the same");
  }
}

defineProps({
  locations: Object,
});
</script>

<template>
  <Head title="Create Bus Route" />
  
  <AuthenticatedLayout>
    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="bg-gray-100 overflow-hidden ma-8 w-100 rounded-lg border shadow-sm">
          <div class="m-6">
            <form class="w-full max-w-sm" @submit.prevent="submit">
              <div class="mb-4">
                <InputLabel for="origin" value="Select Origin:" />
                <select id="origin" v-model="form.origin" class="mt-1 block w-full px-4 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:ring focus:ring-indigo-200 focus:outline-none focus:border-indigo-500">
                  <option v-for="location in locations" :value="location.location">
                    {{ location.location }}
                  </option>
                </select>

                <InputLabel for="destination" value="Select Destination" class="mt-4" />
                <select id="destination" v-model="form.destination" class="mt-1 block w-full px-4 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:ring focus:ring-indigo-200 focus:outline-none focus:border-indigo-500">
                  <option v-for="location in locations" :value="location.location">
                    {{ location.location }}
                  </option>
                </select>
              </div>
              <PrimaryButton type="submit" class="mt-4 flex items-center bg-trymain hover:bg-trysecond text-white font-semibold px-3 py-2 rounded">
                <span class="ml-2">Submit</span>
              </PrimaryButton>
            </form>
          </div>
        </div>
      </div>
    </div>
  </AuthenticatedLayout>
</template>