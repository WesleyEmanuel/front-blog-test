<script>
import CommentCard from "./CommentCard.vue";
export default {
  components: { CommentCard },
  props: {
    comments: {
      type: Array,
      required: true,
    },
  },
};
</script>
<template>
  <v-card class="comments-card" color="#24232b">
    <v-card-text class="d-flex flex-col gap-5">
      <CommentCard
        v-for="comment in comments"
        :key="comment.id"
        :comment="comment"
      />
    </v-card-text>

    <div class="w-3/5 mx-auto m-3">
      <v-card-actions>
        <slot name="actions"></slot>
      </v-card-actions>
    </div>
  </v-card>
</template>

<style>
.comments-card::-webkit-scrollbar {
  width: 15px; /* width of the entire scrollbar */
}
.comments-card::-webkit-scrollbar-track {
  background: #24232b;
}
.comments-card::-webkit-scrollbar-thumb {
  background-color: rgb(134, 79, 236);
  border-radius: 20px;
  border: 3px solid #24232b;
}
</style>
