<script setup>
import { Head, Link } from '@inertiajs/vue3';
import Carousel from '@/Components/Carousel.vue';
defineProps({
    canLogin: {
        type: Boolean,
    },
    canRegister: {
        type: Boolean,
    },

});
</script>
<style>
.inter{
     font-family: 'Inter', sans-serif;
   }
   .k2d-eb{
     font-family: 'K2D', sans-serif;
   }
   .poppins-eb{
     font-family: 'Poppins', sans-serif;
   }
   </style>

]
<template class="w-screen"> 
    <head>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@800&display=swap" rel="stylesheet">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=K2D:wght@800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="/stylesheets/style.css">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter&family=Poppins:ital,wght@0,300;1,200&display=swap" rel="stylesheet">
    </head>

<nav class="bg-gradient bg-trymain
            fixed top-0 z-50 w-full ">
  <div class="px-3 py-3 lg:px-5 lg:pl-3">
        <div class="flex items-center justify-between">
                <div class="flex items-center justify-start">
                    <Link href="/" class="flex ml-2 md:mr-24">
                    
                    <span class="self-center text-xl font-semibold sm:text-2xl whitespace-nowrap text-white k2d-eb"><font-awesome-icon :icon="['fas', 'right-to-bracket']" />taHack transportation</span>
                    </Link>
                </div>
                <div class="flex items-center">
                        <div v-if="canLogin" class="sm:fixed sm:top-0 sm:right-0 p-3 text-right">
                                <Link
                                    v-if="$page.props.auth.user"
                                    :href="route('dashboard')"
                                    class="k2d-eb text-2xl text-white "
                                    >Dashboard</Link
                                >

                                <template v-else>
                                    <div class="flex justify-between">
                                    <Link
                                        :href="route('login')"
                                        class="flex self-center text-base text-white mr-2
                                               "
                                        >
                                        <button
                                        id="navAction"
                                        class="mx-auto  hover:bg-white hover:text-gray-800 text-white poppins-eb rounded-full p-2 opacity-75  transform transition hover:scale-105 duration-300 ease-in-out"
                                    >
                                        Login
                                    </button>
                                    </Link>

                                    <Link
                                        v-if="canRegister"
                                        :href="route('register')"
                                        class="flex text-base text-white "
                                        ><button
                                        id="navAction"
                                        class="mx-auto  hover:bg-white hover:text-gray-800 text-white poppins-eb rounded-full p-2 opacity-75  transform transition hover:scale-105 duration-300 ease-in-out"
                                    >
                                        Sign Up
                                    </button>
                                        </Link
                                    >
                                    
                                    </div>
                                </template>
                        </div>
                </div>
        </div>
  </div>
</nav>

<div class="p-6 dark:border-gray-700 mt-14 bg-blue-400">
    <div class="grid grid-cols-2 md:grid-cols-3 gap-4">
        <div>
            <img class="h-auto max-w-full rounded-lg" src="https://nr4kmtcwpy93.objectstorage.ap-tokyo-1.oci.customer-oci.com/n/nr4kmtcwpy93/b/bucket-20230809-1910/o/carousel1.jpg" alt="">
        </div>
        <div>
            <img class="h-auto max-w-full rounded-lg" src="https://nr4kmtcwpy93.objectstorage.ap-tokyo-1.oci.customer-oci.com/n/nr4kmtcwpy93/b/bucket-20230809-1910/o/carousel1.png" alt="">
        </div>
        <div>
            <img class="h-auto max-w-full rounded-lg" src="https://nr4kmtcwpy93.objectstorage.ap-tokyo-1.oci.customer-oci.com/n/nr4kmtcwpy93/b/bucket-20230809-1910/o/carousel2.jpg" alt="">
        </div>
        <div>
            <img class="h-auto max-w-full rounded-lg" src="https://nr4kmtcwpy93.objectstorage.ap-tokyo-1.oci.customer-oci.com/n/nr4kmtcwpy93/b/bucket-20230809-1910/o/carousel3.jpg" alt="">
        </div>
        <div class="flex justify-center items-center">
            <!-- Assuming Carousel is a component -->
            <Carousel />
        </div>
        <div>
            <img class="h-auto max-w-full rounded-lg" src="https://nr4kmtcwpy93.objectstorage.ap-tokyo-1.oci.customer-oci.com/n/nr4kmtcwpy93/b/bucket-20230809-1910/o/carousel1.png" alt="">
        </div>
    </div>
</div>


</template>

<style>


</style>
