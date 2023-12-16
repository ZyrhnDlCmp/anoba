<script setup>
import {ref} from 'vue';
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
import Dropdown from '@/Components/Dropdown.vue';
import DropdownLink from '@/Components/DropdownLink.vue';
import NavLink from '@/Components/NavLink.vue';
import ResponsiveNavLink from '@/Components/ResponsiveNavLink.vue';
import { Link } from '@inertiajs/vue3';
import Sidebar from '@/Components/Sidebar.vue'
import Navbar from '@/Components/Navbar.vue'
defineProps({
    count_reservation: Number
})

</script>

<template>
    <div>
        <!-- <div class="min-h-screen bg-gray-100"> -->
        <div class="min-h-screen bg-gradient-to-b from-trysecond to-trysecond">
            <Navbar/>
            <Sidebar/>
            <main class="bg-gradient-to-b from-trymain to-trysecond">
                <div class="p-4 sm:ml-64">
                    <div class="p-4 mt-14">
                        <BarChart class="p-3" />
                        <slot/>
                    </div>
                </div>
            </main>
        </div>
    </div>
</template>