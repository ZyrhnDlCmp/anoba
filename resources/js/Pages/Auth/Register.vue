<script setup>
import Checkbox from '@/Components/Checkbox.vue';
import { computed, ref } from 'vue';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';
import VueHcaptcha from '@hcaptcha/vue3-hcaptcha';

const form = useForm({
    name: '',
    email: '',
    password: '',
    password_confirmation: '',
});

const onVerify = (token) => {
    form.post(route('register'), {
        onFinish: () => form.reset('password', 'password_confirmation'),
    });
};
const showPassword = ref(false);

const passwordInputType = computed(() => {
  return showPassword.value ? '' : 'password';
});

</script>

<template >
    <GuestLayout>
        <Head title="Register" />

        <form @submit.prevent="submit" > 

            <div class="flex flex-row">
                 <div class="mt-2">
                    <InputLabel class="poppins-eb" for="name" value="Name" />

                    <TextInput
                        id="name"
                        type="text"
                        class="mt-1 block w-full"
                        v-model="form.name"
                        required
                        autofocus
                        autocomplete="name"
                    />

                    <InputError class="mt-2" :message="form.errors.name" />
                </div>

                <div class="mt-2 ml-2">
                    <InputLabel class="poppins-eb" for="email" value="Email" />

                    <TextInput
                        id="email"
                        type="email"
                        class="mt-1 block w-full"
                        v-model="form.email"
                        required
                        autocomplete="username"
                    />

                    <InputError class="mt-2" :message="form.errors.email" />
                </div>

            </div>
           
            <div class="flex flex-row">
                <div class="mt-4">
                    <InputLabel class="poppins-eb" for="password" value="Password" />

                    <TextInput
                        id="password"
                        :type="passwordInputType"
                        class="mt-1 block w-full"
                        v-model="form.password"
                        required
                        autocomplete="new-password"
                    />

                    <InputError class="mt-2" :message="form.errors.password" />
                </div>

                <div class="mt-4 ml-2">
                    <InputLabel class="poppins-eb" for="password_confirmation" value="Confirm Password" />

                    <TextInput
                        id="password_confirmation"
                        :type="passwordInputType"
                        class="mt-1 block w-full"
                        v-model="form.password_confirmation"
                        required
                        autocomplete="new-password"
                    />

                    <InputError class="mt-2" :message="form.errors.password_confirmation" />
                </div>
            </div>
            

            <label class="flex items-center justify-between mt-2">
                <div class="flex items-center">
                    <Checkbox class="text-trymain focus:ring-trymain" v-model:checked="showPassword" />
                    <span class="ml-2 text-sm text-gray-600 inter">Show Password</span>
                </div>
            </label>

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
                    :href="route('login')"
                    class="underline inter text-sm text-gray-600 hover:text-gray-900 rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
                >
                    Already registered?
                </Link>

                <PrimaryButton class="ml-4 k2d-eb bg-trymainSecond hover:bg-trymain" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    Register
                </PrimaryButton>
            </div>
        </form>
    </GuestLayout>
</template>