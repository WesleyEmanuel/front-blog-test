<script>
export default {
  props: {
    comment: {
      type: Object,
      required: true,
    },
  },
};
</script>
<template>
  <div class="w-full bg-purple-700 text-white p-5 rounded-md">
    <header
      class="flex items-center gap-5 cursor-pointer mb-3 bg-purple-900 p-2 rounded-lg w-auto"
    >
      <div class="hidden xsm:block w-8 h-8 rounded-full bg-slate-400">
        <img src="../assets/default-user.png" alt="" />
      </div>
      <p class="italic text-sm">{{ comment.email }}</p>
    </header>
    <div>
      <h3 class="text-lg font-bold">
        {{ comment.name[0].toUpperCase() + comment.name.substring(1) }}
      </h3>
      <p class="font-extralight mt-1">
        {{ comment.body[0].toUpperCase() + comment.body.substring(1) }}
      </p>
    </div>
  </div>
</template>
