<script setup>
const getWordsNumber = (str) => str.split(" ").length;
</script>

<template>
  <div
    :id="id"
    class="border rounded-md mb-4 p-4 shadow-sm cursor-pointer"
    @click="$router.push(`/posts/${id}`)"
  >
    <h1 class="text-slate-600 text-2xl xl:text-4xl font-medium mb-3">
      {{ title }}
    </h1>
    <p class="text-justify">{{ getWordsNumber(description) }} Words</p>
  </div>
</template>

<script>
export default {
  props: {
    id: Number,
    title: String,
    description: String,
    date: TimeRanges,
  },
};
</script>
