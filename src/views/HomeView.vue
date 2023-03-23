<script>
import api from "../api";
import PostContainer from "../components/PostContainer.vue";
import PostComments from "../components/CommentsContainer.vue";
export default {
  components: {
    PostContainer,
    PostComments,
  },
  data() {
    return {
      commentsDialog: [],
      posts: [],
      users: [],
      postComments: [],
    };
  },
  computed: {},
  beforeMount() {
    this.getPosts();
    this.getUsers();
  },
  methods: {
    userDetails(id) {
      const user = this.users.filter((user) => user.id == id);
      return user[0];
    },
    openCommentsPost({ id, comments }) {
      this.postComments = comments;
      this.commentsDialog[id] = true;
    },
    getPosts() {
      api.get("/posts").then((resp) => {
        this.posts = resp.data;
      });
    },
    getUsers() {
      api.get("/users").then((resp) => {
        this.users = resp.data;
      });
    },
  },
};
</script>

<template>
  <header class="text-center font-extrabold text-5xl m-10 cursor-pointer">
    <h1 class="text-purple-400">Post<b class="text-white">Blog</b></h1>
  </header>
  <main class="p-10">
    <div class="grid grid-cols-1 lg:grid-cols-2 xl:grid-cols-3 gap-20">
      <div v-for="post in posts">
        <PostContainer
          :post="post"
          :userDetails="userDetails(post.userId)"
          @openCommentsPost="openCommentsPost"
        />
        <v-dialog
          v-model="commentsDialog[post.id]"
          width="600"
          class="h-4/5 my-auto"
        >
          <PostComments :comments="postComments">
            <template v-slot:actions>
              <v-btn
                block
                @click="commentsDialog[post.id] = false"
                class="m-auto"
              >
                <b class="text-lg">✖</b>
              </v-btn>
            </template>
          </PostComments>
        </v-dialog>
      </div>
    </div>
  </main>
</template>
