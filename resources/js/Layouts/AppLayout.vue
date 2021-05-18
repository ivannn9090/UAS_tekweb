<template>
  <div class="bg-gray-100 font-family-karla flex">
    <aside class="relative bg-sidebar h-screen w-64 hidden sm:block shadow-xl">
      <div class="p-6">
        <a
          href="index.html"
          class="text-white text-3xl font-semibold uppercase hover:text-gray-300"
          >Trindo</a
        >
      </div>
      <nav class="text-white text-base font-semibold pt-3">
        <a
          :href="route('dashboard')"
          :active="route().current('dashboard')"
          class="flex items-center text-white opacity-75 hover:opacity-100 py-4 pl-6 nav-item"
          ><i class="fas fa-tachometer-alt mr-3"></i>
          Dashboard
        </a>
        <a
          href="/posts"
          :active="route().current('posts.index')"
          class="flex items-center text-white opacity-75 hover:opacity-100 py-4 pl-6 nav-item"
          ><i class="fas fa-clipboard-list mr-3"></i>
          Post
        </a>
        <a
          href="/"
          :active="route().current('blog.index')"
          class="flex items-center text-white opacity-75 hover:opacity-100 py-4 pl-6 nav-item"
          ><i class="fas fa-globe mr-3"></i>
          Website
        </a>
      </nav>
    </aside>

    <div class="w-full flex flex-col h-screen overflow-y-hidden">
      <!-- Desktop Header -->
      <header class="w-full items-center bg-white py-2 px-6 hidden sm:flex">
        <div class="w-1/2"></div>
        <div x-data="{ isOpen: false }" class="relative w-1/2 flex justify-end">
          <!-- Settings Dropdown -->
          <div class="ml-3 relative">
            <jet-dropdown align="right" width="48">
              <template #trigger>
                <button
                  v-if="$page.props.jetstream.managesProfilePhotos"
                  class="flex text-sm border-2 border-transparent rounded-full focus:outline-none focus:border-gray-300 transition"
                >
                  <img
                    class="h-8 w-8 rounded-full object-cover"
                    :src="$page.props.user.profile_photo_url"
                    :alt="$page.props.user.name"
                  />
                </button>

                <span v-else class="inline-flex rounded-md">
                  <button
                    type="button"
                    class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded-md text-gray-500 bg-white hover:text-gray-700 focus:outline-none transition"
                  >
                    {{ $page.props.user.name }}

                    <svg
                      class="ml-2 -mr-0.5 h-4 w-4"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                      fill="currentColor"
                    >
                      <path
                        fill-rule="evenodd"
                        d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                        clip-rule="evenodd"
                      />
                    </svg>
                  </button>
                </span>
              </template>

              <template #content>
                <!-- Account Management -->
                <div class="block px-4 py-2 text-xs text-gray-400">
                  Manage Account
                </div>

                <jet-dropdown-link :href="route('profile.show')">
                  Profile
                </jet-dropdown-link>

                <jet-dropdown-link
                  :href="route('api-tokens.index')"
                  v-if="$page.props.jetstream.hasApiFeatures"
                >
                  API Tokens
                </jet-dropdown-link>

                <div class="border-t border-gray-100"></div>

                <!-- Authentication -->
                <form @submit.prevent="logout">
                  <jet-dropdown-link as="button"> Log Out </jet-dropdown-link>
                </form>
              </template>
            </jet-dropdown>
          </div>
        </div>
      </header>

      <!-- Mobile Header & Nav -->
      <header
        x-data="{ isOpen: false }"
        class="w-full bg-sidebar py-5 px-6 sm:hidden"
      >
        <div class="flex items-center justify-between">
          <a
            class="text-white text-3xl font-semibold uppercase hover:text-gray-300"
            >TRINDO</a
          >
          <!-- <button
            @click="isOpen = !isOpen"
            class="text-white text-3xl focus:outline-none"
          >
            <i x-show="!isOpen" class="fas fa-bars"></i>
            <i x-show="isOpen" class="fas fa-times"></i>
          </button> -->
        </div>

        <!-- Dropdown Nav -->
        <!-- <nav :class="isOpen ? 'flex' : 'hidden'" class="flex flex-col pt-4"> -->
        <a
          :href="route('dashboard')"
          :active="route().current('dashboard')"
          class="flex items-center text-white opacity-75 hover:opacity-100 py-4 pl-6 nav-item"
          ><i class="fas fa-tachometer-alt mr-3"></i>
          Dashboard
        </a>
        <a
          href="/posts"
          :active="route().current('posts.index')"
          class="flex items-center text-white opacity-75 hover:opacity-100 py-4 pl-6 nav-item"
          ><i class="fas fa-clipboard-list mr-3"></i>
          Post
        </a>
        <a
          href="/"
          :active="route().current('blog.index')"
          class="flex items-center text-white opacity-75 hover:opacity-100 py-4 pl-6 nav-item"
          ><i class="fas fa-globe mr-3"></i>
          Website
        </a>
        <!-- </nav> -->
        <!-- <button class="w-full bg-white cta-btn font-semibold py-2 mt-5 rounded-br-lg rounded-bl-lg rounded-tr-lg shadow-lg hover:shadow-xl hover:bg-gray-300 flex items-center justify-center">
                <i class="fas fa-plus mr-3"></i> New Report
            </button> -->
      </header>

      <div class="w-full overflow-x-hidden border-t flex flex-col">
        <!-- Page Heading -->
        <header class="bg-white shadow" v-if="$slots.header">
          <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
            <slot name="header"></slot>
          </div>
        </header>
        <!-- Page Content -->
        <main>
          <slot></slot>
        </main>
      </div>
    </div>
  </div>
</template>

<script>
import JetApplicationMark from "@/Jetstream/ApplicationMark";
import JetBanner from "@/Jetstream/Banner";
import JetDropdown from "@/Jetstream/Dropdown";
import JetDropdownLink from "@/Jetstream/DropdownLink";
import JetNavLink from "@/Jetstream/NavLink";
import JetResponsiveNavLink from "@/Jetstream/ResponsiveNavLink";

export default {
  components: {
    JetApplicationMark,
    JetBanner,
    JetDropdown,
    JetDropdownLink,
    JetNavLink,
    JetResponsiveNavLink,
  },

  data() {
    return {
      showingNavigationDropdown: false,
    };
  },

  methods: {
    switchToTeam(team) {
      this.$inertia.put(
        route("current-team.update"),
        {
          team_id: team.id,
        },
        {
          preserveState: false,
        }
      );
    },

    logout() {
      this.$inertia.post(route("logout"));
    },
  },
};
</script>
