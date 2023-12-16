
<script setup>
import Checkbox from '@/Components/Checkbox.vue';
import { computed, ref } from 'vue';

import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import VueHcaptcha from '@hcaptcha/vue3-hcaptcha';
import { Head, Link, useForm } from '@inertiajs/vue3';

defineProps({
    canResetPassword: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});

const form = useForm({
    email: '',
    password: '',
    remember: false,
});

const showPassword = ref(false);



const onVerify = (token) => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};

const submit = () => {
    onVerify();
};

const passwordInputType = computed(() => (showPassword.value ? 'text' : 'password'));

</script>

<template>
    <GuestLayout>
        <Head title="Log in" />

        <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
            {{ status }}
        </div>
        
        
        <form @submit.prevent="submit">
            <div>
                <InputLabel class="poppins-eb" for="email" value="Email" />

                <TextInput
                    id="email"
                    type="email"
                    class="mt-1 block w-full"
                    v-model="form.email"
                    required
                    autofocus
                    autocomplete="username"
                />

                <InputError class="mt-2" :message="form.errors.email" />
            </div>

            <div class="mt-4">
                <InputLabel class="poppins-eb" for="password" value="Password" />

                <TextInput 
                    id="password"
                    :type="passwordInputType"
                    class="mt-1 block w-full focus:ring-trymain"
                    v-model="form.password"
                    required
                    autocomplete="current-password"
                />

                <InputError class="mt-2" :message="form.errors.password" />
            </div>
            <div class="block mt-4">
                <label class="flex items-center justify-between">
                    <div class="flex items-center">
                        <Checkbox class="focus:ring-trymain text-trymain" v-model:checked="showPassword" />
                        <span class="ml-2 text-sm text-gray-600 inter ">Show Password</span>
                    </div>
                    <div class="flex items-center">
                        <Checkbox class="focus:ring-trymain text-trymain"  name="remember" v-model:checked="form.remember" />
                        <span class="ml-2 text-sm text-gray-600 inter">Remember me</span>
                    </div>
                </label>
            </div>

            
            <div class="mt-4 flex justify-center items-center">
                <VueHcaptcha
                    sitekey="1d151931-97dd-41a5-be11-18a8599a3632"
                    @verify="onVerify"
                    @expired="onExpire"
                    @challenge-expired="onChallengeExpire"
                    @error="onError"
                ></VueHcaptcha>
            </div>


            

            <div class="flex items-center justify-end mt-4">
                <Link
                    v-if="canResetPassword"
                    :href="route('password.request')"
                    class="underline text-sm inter text-gray-600 hover:text-gray-900 rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-trymain"
                >
                    Forgot your password?
                </Link>

                <PrimaryButton class="ml-4 bg-trymainSecond hover:bg-trymain k2d-eb" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    Log in
                </PrimaryButton>
            </div>
        </form>
    </GuestLayout>
</template>

