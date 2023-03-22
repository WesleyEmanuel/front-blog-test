<script>
import api from "../api";
import PostContainer from "../components/PostContainer.vue";
import PostComments from "../components/PostCommentsContainer.vue";
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
  <main class="p-10">
    <div class="grid grid-cols-1 lg:grid-cols-2 xl:grid-cols-3 gap-20">
      <div v-for="post in posts">
        <PostContainer
          :post="post"
          :userDetails="userDetails(post.userId)"
          @openCommentsPost="openCommentsPost"
        />
        <v-dialog v-model="commentsDialog[post.id]" width="600">
          <PostComments :comments="postComments">
            <template v-slot:actions>
              <v-btn
                color="white"
                block
                @click="commentsDialog[post.id] = false"
                class="m-auto"
                >Close Comments</v-btn
              >
            </template>
          </PostComments>
        </v-dialog>
      </div>
    </div>
  </main>
</template>
