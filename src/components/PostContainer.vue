<script>
import api from "../api";

export default {
  props: {
    post: {
      type: Object,
      required: true,
    },
    userDetails: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      users: [],
      comments: [],
    };
  },
  methods: {
    getPostComments(id) {
      api.get(`/posts/${id}/comments`).then((resp) => {
        this.comments = resp.data;
      });
    },
  },
  mounted() {
    this.getPostComments(this.post.id);
  },
};
</script>
<template>
  <div
    class="sm mx-auto px-10 py-20 shadow-sm shadow-violet-400 rounded-md text-white cursor-pointer hover:translate-y-[-5px] transition duration-150"
    @click="$emit('openCommentsPost', { id: post.id, comments })"
  >
    <header class="mb-4 text-2xl font-bold text-violet-400">
      <h3>{{ post.title[0].toUpperCase() + post.title.substring(1) }}</h3>
    </header>
    <main class="my-7">
      <p>{{ post.body[0].toUpperCase() + post.body.substring(1) }}</p>
    </main>
    <footer class="mt-7 flex justify-between items-center">
      <div class="flex items-center gap-3">
        <div class="w-8 h-8 rounded-full bg-slate-400">
          <img src="../assets/default-user.png" alt="" />
        </div>
        <div>
          <p>{{ userDetails && userDetails.name }}</p>
          <p class="italic font-light">
            {{ userDetails && userDetails.email }}
          </p>
        </div>
      </div>
      <div class="hidden md:block">
        <p>{{ comments.length + " comments" }}</p>
      </div>
    </footer>
  </div>
</template>
