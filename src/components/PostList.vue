<template>
  <div v-if="posts.length > 0">
    <h3>Список постов</h3>
    <div
      class="post-list"
    >
      <post-item
        v-for="post in posts"
        :post
        :key="post.id"
        @remove="$emit('remove', post)"
      >
      </post-item>
    </div>
  </div>
  <h2 v-else style="color: red">
    Список постов пуст
  </h2>
</template>

<script>
import PostItem from "@/components/PostItem.vue";

export default {
  components: {PostItem},
  props: {
    posts: {
      type: Array,
      required: true,
    }
  }
}
</script>

<style scoped>
  .post-list {
    display: flex;
    justify-content: flex-start;
    gap: 10px;
    flex-wrap: wrap;
  }
</style>
