<template>
  <div>
    <!-- Top Bar Nav -->
    <nav class="w-full py-4 bg-blue-800 shadow">
      <div
        class="
          w-full
          container
          mx-auto
          flex flex-wrap
          items-center
          justify-between
        "
      >
        <nav>
          <ul
            class="
              flex
              items-center
              justify-between
              font-bold
              text-sm text-white
              uppercase
              no-underline
            "
            v-if="!$page.props.user"
          >
            <li>
              <a href="/login">login</a>
            </li>
          </ul>
          <ul
            class="
              flex
              items-center
              justify-between
              font-bold
              text-sm text-white
              uppercase
              no-underline
            "
            v-if="$page.props.user"
          >
            <li>
              <a class="bg-blue-800" href="/dashboard">Dashboard</a>
            </li>
            ||
            <li>
              <inertia-link class="bg-blue-800" href="/logout" method="post"
                >logout</inertia-link
              >
            </li>
          </ul>
        </nav>

        <div class="flex items-center text-lg no-underline text-white pr-6">
          <a class="" href="#">
            <i class="fab fa-facebook"></i>
          </a>
          <a class="pl-6" href="#">
            <i class="fab fa-instagram"></i>
          </a>
          <a class="pl-6" href="#">
            <i class="fab fa-twitter"></i>
          </a>
          <a class="pl-6" href="#">
            <i class="fab fa-linkedin"></i>
          </a>
        </div>
      </div>
    </nav>

    <!-- Text Header -->
    <header class="w-full container mx-auto">
      <div class="flex flex-col items-center py-12">
        <inertia-link
          :href="`/`"
          class="font-bold text-gray-800 uppercase hover:text-gray-700 text-5xl"
        >
          Travel Indonesia
        </inertia-link>
        <p class="text-lg text-gray-600">By : Andi Muh Richvan Junaid</p>
      </div>
    </header>

    <!-- Topic Nav -->
    <nav
      class="w-full py-4 border-t border-b bg-gray-100"
      x-data="{ open: false }"
    >
      <div class="block sm:hidden">
        <a
          href="#"
          class="
            block
            md:hidden
            text-base
            font-bold
            uppercase
            text-center
            flex
            justify-center
            items-center
          "
          @click="open = !open"
        >
          Topics
          <i class="fas ml-2"></i>
        </a>
      </div>
      <div class="w-full flex-grow sm:flex sm:items-center sm:w-auto">
        <div
          class="
            w-full
            container
            mx-auto
            flex flex-col
            sm:flex-row
            items-center
            justify-center
            text-sm
            font-bold
            uppercase
            mt-0
            px-6
            py-2
          "
        >
          <a href="#" class="hover:bg-gray-400 rounded py-2 px-4 mx-2"
            >Technology</a
          >
          <a href="#" class="hover:bg-gray-400 rounded py-2 px-4 mx-2"
            >Automotive</a
          >
          <a href="#" class="hover:bg-gray-400 rounded py-2 px-4 mx-2"
            >Finance</a
          >
          <a href="#" class="hover:bg-gray-400 rounded py-2 px-4 mx-2"
            >Politics</a
          >
          <a href="#" class="hover:bg-gray-400 rounded py-2 px-4 mx-2"
            >Culture</a
          >
          <a href="#" class="hover:bg-gray-400 rounded py-2 px-4 mx-2"
            >Sports</a
          >
        </div>
      </div>
    </nav>

    <div class="container mx-auto flex flex-wrap py-6">
      <!-- Posts Section -->
      <section class="w-full md:w-2/3 flex flex-col items-center px-3">
        <!-- Page Content -->
        <main>
          <slot></slot>
        </main>

        <!-- Model Portal -->
        <portal-target name="model"> </portal-target>
      </section>

      <!-- Sidebar Section -->
      <aside class="w-full md:w-1/3 flex flex-col items-center px-3"></aside>
    </div>

    <footer class="w-full border-t bg-white pb-12">
      <div class="w-full container mx-auto flex flex-col items-center">
        <div class="uppercase pb-6">&copy; Travelindo.com</div>
      </div>
    </footer>
  </div>
</template>