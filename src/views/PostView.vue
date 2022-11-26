<script setup>
import { reactive } from "vue";
import { useRoute } from "vue-router";
import store from "../store";
import supabase from "../supabase";

const route = useRoute();

let post = reactive({});

const fetchPost = async (id) => {
  const found = store.posts.find(
    (item) => item.id === parseInt(route.params.id)
  );

  if (found) {
    return;
  }

  let { data, error } = await supabase
    .from("posts")
    .select()
    .eq("id", id)
    .single();

  if (error) throw new Error(error);

  Object.assign(post, data);

  store.posts = [...store.posts, data];
  console.log(post);
};

fetchPost(route.params.id);
</script>

<template>
  <div v-if="!post">There's is no data</div>
  <div v-else>
    <div class="max-w-[600px] mx-5 md:max-w-[800px] md:mx-auto">
      <div :key="post.id" class="mb-4 p-4 space-y-4">
        <h1 class="text-slate-600 text-xl md:text-3xl font-medium">
          {{ post.title }}
        </h1>
        <p class="text-justify">{{ post.description }}</p>
        <p class="text-center">{{ post.date }}</p>
        <button @click="$router.push('/')" class="underline underline-offset-2">
          Back
        </button>
      </div>
    </div>
  </div>
</template>
