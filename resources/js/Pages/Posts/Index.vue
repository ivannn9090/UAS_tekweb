<template>
  <app-layout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">Post</h2>
    </template>
    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
          <div class="p-6 sm:px-20 bg-white border-b border-gray-200 pb-20">
            <div class="mt-8 mb-8 text-2xl">list of Post</div>
            <div class="mt-8 mb-8">
              <inertia-link
                :href="`/posts/create`"
                class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded my-3"
                >Create New Post</inertia-link
              >
            </div>
            <div
              class="bg-blue-100 border-t-4 border-teal-500 rounded-b text-teal-900 px-4 py-3 shadow-md my-3"
              role="alert"
              v-if="$page.props.success.message"
            >
              <div class="flex">
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
                <th class="bg-gray-200 border px-8 py-4">Title</th>
                <th class="bg-gray-200 border px-8 py-4">Author</th>
                <th class="bg-gray-200 border px-8 py-4">published At</th>
                <th class="bg-gray-200 border px-8 py-4" width="20%">action</th>
              </tr>
              <tr v-for="post in posts.data" :key="post.id">
                <td class="border text-left px-8 py-4">{{ post.title }}</td>
                <td class="border text-left px-8 py-4">
                  {{ post.user.name }}
                </td>
                <td class="border text-left px-8 py-4">
                  {{ post.published_at }}
                </td>
                <td class="border text-left px-8 py-4">
                  <inertia-link
                    :href="`/posts/${post.id}/edit`"
                    class="bg-blue-500 hover:bg-blue-700 text-white py-1 px-3 rounded"
                    >Edith</inertia-link
                  >
                  <button
                    @click="deletePost(post)"
                    class="bg-red-500 hover:bg-red-700 text-white py-1 px-3 rounded"
                  >
                    Delete
                  </button>
                </td>
              </tr>
            </table>
            <div class="mt-8">
              <pagination :links="posts.links"></pagination>
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
