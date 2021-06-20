<template>
  <jet-authentication-card>
    <!-- <body
      class="body-bg min-h-screen pt-12 md:pt-20 pb-6 px-2 md:px-0"
      style="font-family: 'Lato', sans-serif"
    > -->
    <!-- <header class="max-w-lg mx-auto">
      <a href="#">
        <h1 class="text-4xl font-bold text-white text-center">Startup</h1>
      </a>
    </header> -->

    <!-- <main
      class="bg-white max-w-lg mx-auto p-8 md:p-12 my-10 rounded-lg shadow-2xl"
    > -->
    <section>
      <h3 class="font-bold text-2xl">Welcome to Startup</h3>
      <p class="text-gray-600 pt-2">Sign in to your account.</p>
    </section>

    <section class="mt-10">
      <form class="flex flex-col" @submit.prevent="submit">
        <div class="mb-6 pt-3 rounded bg-gray-200">
          <jet-label for="email" value="Email" />
          <jet-input
            id="email"
            type="email"
            class="bg-gray-200 rounded w-full text-gray-700 focus:outline-none border-b-4 border-gray-300 focus:border-purple-600 transition duration-500 px-3 pb-3"
            v-model="form.email"
            required
            autofocus
          />

          <!-- <label
            class="block text-gray-700 text-sm font-bold mb-2 ml-3"
            for="email"
            >Email</label
          >
          <input
            type="text"
            id="email"
            class="bg-gray-200 rounded w-full text-gray-700 focus:outline-none border-b-4 border-gray-300 focus:border-purple-600 transition duration-500 px-3 pb-3"
          /> -->
        </div>
        <div class="mb-6 pt-3 rounded bg-gray-200">
          <jet-label for="password" value="Password" />
          <jet-input
            id="password"
            type="password"
            class="bg-gray-200 rounded w-full text-gray-700 focus:outline-none border-b-4 border-gray-300 focus:border-purple-600 transition duration-500 px-3 pb-3"
            v-model="form.password"
            required
            autocomplete="current-password"
          />

          <!-- <label
            class="block text-gray-700 text-sm font-bold mb-2 ml-3"
            for="password"
            >Password</label
          >
          <input
            type="password"
            id="password"
            class="bg-gray-200 rounded w-full text-gray-700 focus:outline-none border-b-4 border-gray-300 focus:border-purple-600 transition duration-500 px-3 pb-3"
          /> -->
        </div>

        <div class="block mt-4">
          <label class="flex items-center">
            <jet-checkbox name="remember" v-model:checked="form.remember" />
            <span class="ml-2 text-sm text-gray-600">Remember me</span>
          </label>
        </div>

        <div class="flex justify-end">
          <inertia-link
            v-if="canResetPassword"
            :href="route('password.request')"
            class="underline text-sm text-gray-600 hover:text-gray-900"
          >
            Forgot your password?
          </inertia-link>
        </div>
        <!-- <button
          class="bg-purple-600 hover:bg-purple-700 text-white font-bold py-2 rounded shadow-lg hover:shadow-xl transition duration-200"
          type="submit"
        >
          Sign In
        </button> -->
        <jet-button
          class="text-center bg-purple-600 hover:bg-purple-700 text-white font-bold py-2 rounded shadow-lg hover:shadow-xl transition duration-200"
          :class="{ 'opacity-25': form.processing }"
          :disabled="form.processing"
        >
          Log in
        </jet-button>
      </form>
    </section>
    <!-- </main> -->

    <!-- <div class="max-w-lg mx-auto text-center mt-12 mb-6">
      <p class="text-white">
        Don't have an account?
        <a href="#" class="font-bold hover:underline">Sign up</a>.
      </p>
    </div> -->

    <!-- <footer class="max-w-lg mx-auto flex justify-center text-white">
      <a href="#" class="hover:underline">Contact</a>
      <span class="mx-3">•</span>
      <a href="#" class="hover:underline">Privacy</a>
    </footer> -->
    <!-- </body> -->

    <!-- <template #logo>
      <jet-authentication-card-logo />
    </template>

    <jet-validation-errors class="mb-4" />

    <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
      {{ status }}
    </div>

    <form @submit.prevent="submit">
      <div>
        <jet-label for="email" value="Email" />
        <jet-input
          id="email"
          type="email"
          class="mt-1 block w-full"
          v-model="form.email"
          required
          autofocus
        />
      </div>

      <div class="mt-4">
        <jet-label for="password" value="Password" />
        <jet-input
          id="password"
          type="password"
          class="mt-1 block w-full"
          v-model="form.password"
          required
          autocomplete="current-password"
        />
      </div>

      <div class="block mt-4">
        <label class="flex items-center">
          <jet-checkbox name="remember" v-model:checked="form.remember" />
          <span class="ml-2 text-sm text-gray-600">Remember me</span>
        </label>
      </div>

      <div class="flex items-center justify-end mt-4">
        <inertia-link
          v-if="canResetPassword"
          :href="route('password.request')"
          class="underline text-sm text-gray-600 hover:text-gray-900"
        >
          Forgot your password?
        </inertia-link>

        <jet-button
          class="ml-4"
          :class="{ 'opacity-25': form.processing }"
          :disabled="form.processing"
        >
          Log in
        </jet-button>
      </div>
    </form> -->
  </jet-authentication-card>
</template>

<script>
import JetAuthenticationCard from "@/Jetstream/AuthenticationCard";
import JetAuthenticationCardLogo from "@/Jetstream/AuthenticationCardLogo";
import JetButton from "@/Jetstream/Button";
import JetInput from "@/Jetstream/Input";
import JetCheckbox from "@/Jetstream/Checkbox";
import JetLabel from "@/Jetstream/Label";
import JetValidationErrors from "@/Jetstream/ValidationErrors";

export default {
  components: {
    JetAuthenticationCard,
    JetAuthenticationCardLogo,
    JetButton,
    JetInput,
    JetCheckbox,
    JetLabel,
    JetValidationErrors,
  },

  props: {
    canResetPassword: Boolean,
    status: String,
  },

  data() {
    return {
      form: this.$inertia.form({
        email: "",
        password: "",
        remember: false,
      }),
    };
  },

  methods: {
    submit() {
      this.form
        .transform((data) => ({
          ...data,
          remember: this.form.remember ? "on" : "",
        }))
        .post(this.route("login"), {
          onFinish: () => this.form.reset("password"),
        });
    },
  },
};
</script>
