<script setup>
import PostItem from "../components/PostItem.vue";
import supabase from "../supabase";

import store from "../store.js";

const fetchPosts = async () => {
  let { data: posts, error } = await supabase.from("posts").select();

  if (error) throw new Error(error);

  store.posts = posts;
};

fetchPosts();
</script>

<template>
  <div class="Home">
    <div class="max-w-[600px] mx-5 xl:max-w-[800px] xl:mx-auto">
      <main>
        <div v-if="!store.posts.length">There's no Posts</div>
        <div v-else>
          <div
            class="post-item"
            v-for="(item, index) in store.posts"
            :key="index"
          >
            <PostItem
              :id="item.id"
              :title="item.title"
              :description="item.description"
            />
          </div>
        </div>
      </main>
    </div>
  </div>
</template>
