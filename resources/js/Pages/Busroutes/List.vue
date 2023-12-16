

<template>
    <Head title="Bus Routes" />
  
    <AuthenticatedLayout>
      <div class="py-12">
        <div class="max-auto mx-auto sm:px-6 lg:px-8 px-4 px-6">
          <div class="bg-gray-100 overflow-hidden shadow-sm sm:rounded-lg px-2 py-6 ">
            <div class="p-3">
              <Link
                :href="route('busroutes.create')"
                class="flex items-center bg-trythird hover:bg-trysecond text-white font-semibold px-3 py-2 rounded mx-2"
                as="button"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke-width="1.5"
                  stroke="currentColor"
                  class="w-5 h-5 mr-2"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M12 9v6m3-3H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z"
                  />
                </svg>
                Add New
              </Link>
            </div>
  
            <div class="p-6 text-gray-900">
              <div class="overflow-x-auto w-full">
                <div class="space-y-4">
                  <div
                    v-for="busroute in busroutes"
                    :key="busroute.id"
                    class="bg-white rounded-lg text-trymain shadow-md duration-300 ease-in-out dark:bg-gray-800"
                  >
                    <div @click="toggleAccordion(busroute.id)" class="cursor-pointer">
                      <div class="flex justify-between items-center p-4">
                        <h3 class="text-lg font-semibold">{{ busroute.origin }} to {{ busroute.destination }}</h3>
                        <span class="text-trythird">
                        <svg
                          xmlns="http://www.w3.org/2000/svg"
                          :class="{'transform rotate-180': activeAccordion === busroute.id, 'transform rotate-0': activeAccordion !== busroute.id}"
                          fill="none"
                          viewBox="0 0 24 24"
                          stroke="currentColor"
                          class="w-6 h-6"
                        >
                          <path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" />
                        </svg>
                    </span>
                      </div>
                    </div>
                    <div v-if="activeAccordion === busroute.id" class="p-4">
                      <!-- Content for the expanded route card -->
                      <div class="flex">
                        <Link
                          title="Edit Bus Route"
                          :href="route('busroutes.edit', { id: busroute.id })"
                          class="flex items-center bg-trymain hover:bg-trysecond text-white font-semibold px-3 py-2 m-2 rounded mx-2"
                          :data="{ id: busroute.id, locations: busroutes }"
                          as="button"
                        >
                          <svg
                            xmlns="http://www.w3.org/2000/svg"
                            fill="none"
                            viewBox="0 0 24 24"
                            stroke-width="2"
                            stroke="currentColor"
                            class="w-5 h-5"
                          >
                            <path
                              stroke-linecap="round"
                              stroke-linejoin="round"
                              d="M19.5 14.25v-2.625a3.375 3.375 0 00-3.375-3.375h-1.5A1.125 1.125 0 0113.5 7.125v-1.5a3.375 3.375 0 00-3.375-3.375H8.25m0 12.75h7.5m-7.5 3H12M10.5 2.25H5.625c-.621 0-1.125.504-1.125 1.125v17.25c0 .621.504 1.125 1.125 1.125h12.75c.621 0 1.125-.504 1.125-1.125V11.25a9 9 0 00-9-9z"
                            />
                          </svg>
                          <span class="ml-2">Edit Route</span>
                        </Link>
                        <PrimaryButton
                          title="Delete Bus Route"
                          class="flex items-center bg-trysecond hover:bg-trymain text-white font-semibold px-3 py-2 m-2 rounded mx-2"
                          @Click="destroy(busroute.id)"
                        >
                          <svg
                            xmlns="http://www.w3.org/2000/svg"
                            fill="none"
                            viewBox="0 0 24 24"
                            stroke-width="2"
                            stroke="currentColor"
                            class="w-6 h-6"
                          >
                            <path
                              stroke-linecap="round"
                              stroke-linejoin="round"
                              d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0"
                            />
                          </svg>
                          <span class="ml-2">Delete Route</span>
                        </PrimaryButton>
                      </div>
                    </div>
                  </div>
                </div>
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
  import NavLink from '@/Components/NavLink.vue';
  import PrimaryButton from '@/Components/PrimaryButton.vue';
  
  const activeAccordion = ref(null);
  
  defineProps({
    busroutes: Object,
  });
  
  function destroy(id) {
    if (confirm('Are you sure you want to delete this Route?')) {
      router.delete(route('busroutes.destroy', id));
    }
  }
  
  function toggleAccordion(id) {
    activeAccordion.value = activeAccordion.value === id ? null : id;
  }
  </script>