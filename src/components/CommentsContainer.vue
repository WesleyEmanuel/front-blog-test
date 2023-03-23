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

    <div class="mx-auto m-3">
      <v-card-actions>
        <div
          class="fixed top-[-1.7rem] right-[-1.5rem] bg-red w-[2rem] h-[2rem] rounded-[50%]"
        >
          <slot name="actions"></slot>
        </div>
      </v-card-actions>
    </div>
  </v-card>
</template>

<style>
.comments-card::-webkit-scrollbar {
  width: 15px;
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
