<script setup>
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
import { Link } from '@inertiajs/vue3';
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

<template>
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
    <nav class="bg-gradient bg-tahack
            fixed top-0 z-50 w-full ">
  <div class="px-3 py-3 lg:px-5 lg:pl-3">
        <div class="flex items-center justify-between">
                <div class="flex items-center justify-start">
                    <Link href="/" class="flex ml-2 md:mr-24">
                    
                    <span class="self-center text-xl font-semibold sm:text-2xl whitespace-nowrap text-white k2d-eb"><font-awesome-icon :icon="['fas', 'right-to-bracket']" />taHack transportation</span>
                    </Link>
                </div>
                <div class="flex items-center">
                        <div v-if="canLogin" class="sm:fixed sm:top-0 sm:right-0 p-2 text-right">
                                <Link
                                    v-if="$page.props.auth.user"
                                    :href="route('dashboard')"
                                    class="font-semibold text-2xl text-gray-600 hover:text-gray-900 dark:text-gray-400 dark:hover:text-white focus:outline focus:outline-2 focus:rounded-sm focus:outline-red-500"
                                    >Dashboard</Link
                                >

                                <template v-else>
                                    <div class="flex justify-between">
                                    

                                    <Link
                                        v-if="canRegister"
                                        :href="route('register')"
                                        class="flex text-base text-white "
                                        ><button
                                        id="navAction"
                                        class="mx-auto   text-white poppins-eb rounded-full p-2 opacity-75  transform transition hover:scale-105 duration-300 ease-in-out"
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

    <div class="min-h-screen bg-tahack py-4 flex flex-col sm:justify-center rounded-xl items-center pt-6 sm:pt-0">
        

        <div
            class="w-full sm:max-w-md mt-6 px-6 py-4 bg-white rounded-xl shadow-md  justify-center items-center overflow-hidden "
        >
        <div class="w-full flex flex-row justify-center align-center items-center rounded-xl"> 
            <Link href="/">
                <ApplicationLogo class="w-48 h-48 justify-center \" />
            </Link>
        </div>
        
            <slot />
        </div>
    </div>
</template>

