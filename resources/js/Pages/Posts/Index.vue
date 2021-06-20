<template>
  <app-layout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">Post</h2>
    </template>
    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
          <div class="p-6 sm:px-20 bg-white border-b border-gray-200 pb-20">
            <div class="mt-8 mb-8 text-2xl">Daftar Data Post</div>
            <div class="mt-8 mb-8">
              <inertia-link
                :href="`/posts/create`"
                class="
                  bg-blue-500
                  hover:bg-blue-700
                  text-white
                  font-bold
                  py-2
                  px-4
                  rounded
                  my-3
                "
                >Create New Post</inertia-link
              >
            </div>

            <div
              class="
                bg-teal-100
                border-t-4 border-teal-500
                rounded-b
                text-teal-900
                px-4
                py-3
                shadow-md
              "
              role="alert"
              v-if="$page.props.success.message"
            >
              <div class="flex">
                <div class="py-1">
                  <svg
                    class="fill-current h-6 w-6 text-teal-500 mr-4"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                  >
                    <path
                      d="M2.93 17.07A10 10 0 1 1 17.07 2.93 10 10 0 0 1 2.93 17.07zm12.73-1.41A8 8 0 1 0 4.34 4.34a8 8 0 0 0 11.32 11.32zM9 11V9h2v6H9v-4zm0-6h2v2H9V5z"
                    />
                  </svg>
                </div>
                <div>
                  <p class="text-sm">{{ $page.props.success.message }}</p>
                </div>
              </div>
            </div>
            <!-- <div
              v-if="$page.props.flash.message"
              class="bg-teal-100 border-t-4 border-teal-500 rounded-b text-teal-900 px-4 py-3 shadow-md my-3"
              role="alert"
            >
              {{ $page.props.flash.message }}
            </div> -->
            <table class="shadow-lg bg-white w-full">
              <tr>
                <th class="bg-gray-200 border px-8 py-4">Judul</th>
                <th class="bg-gray-200 border px-8 py-4">Author</th>
                <th class="bg-gray-200 border px-8 py-4">published At</th>
                <th class="bg-gray-200 border px-8 py-4" width="25%">action</th>
              </tr>
              <tr v-for="post in posts.data" :key="post.id">
                <td
                  v-show="$page.props.user.id == post.user_id"
                  class="border text-left px-8 py-4"
                >
                  {{ post.title }}
                </td>
                <td
                  v-show="$page.props.user.id == post.user_id"
                  class="border text-left px-8 py-4"
                >
                  {{ post.user.name }}
                </td>
                <td
                  v-show="$page.props.user.id == post.user_id"
                  class="border text-left px-8 py-4"
                >
                  {{ post.published_at }}
                </td>
                <td
                  v-show="$page.props.user.id == post.user_id"
                  class="border text-center px-8 py-4"
                >
                  <inertia-link
                    :href="`/posts/${post.id}/edit`"
                    class="
                      bg-blue-500
                      hover:bg-blue-700
                      text-white
                      py-1
                      px-3
                      rounded
                    "
                    ><i class="far fa-edit"></i
                  ></inertia-link>
                  ||
                  <button
                    @click="deletePost(post)"
                    v-show="$page.props.user.id == post.user_id"
                    class="
                      bg-red-500
                      hover:bg-red-700
                      text-white
                      py-1
                      px-3
                      rounded
                    "
                  >
                    <i class="fas fa-trash"></i>
                  </button>
                  ||
                  <inertia-link
                    :href="`/${post.slug}`"
                    class="
                      bg-green-500
                      hover:bg-blue-700
                      text-white
                      py-1
                      px-3
                      rounded
                    "
                    ><i class="fas fa-globe"></i
                  ></inertia-link>
                </td>
              </tr>
            </table>
            <div class="text-center mt-8">
              <pagination class="text-center" :links="posts.links"></pagination>
            </div>
          </div>
        </div>
      </div>
    </div>
  </app-layout>
</template>

<script>
import Button from "../../Jetstream/Button.vue";
import Pagination from "../Shared/Pagination.vue";
import AppLayout from "./../../Layouts/AppLayout";

export default {
  props: ["posts"],
  components: {
    AppLayout,
    Pagination,
    Button,
  },
  methods: {
    deletePost(data) {
      if (!confirm("are you sure want to delete this ?")) return;

      this.$inertia.delete("/posts/" + data.id);
    },
  },
};
</script>
