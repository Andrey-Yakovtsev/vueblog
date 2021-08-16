<template>
<div v-if="posts.length > 0">
  <h3>Posts list</h3>
  <transition-group name="post-list">
      <post-item
      :post="post"
      v-for="post in posts"
      :key="post.id"
      @remove="$emit('remove', post)"
  ></post-item>
  </transition-group>

</div>
  <h3 v-else style="color: red"> Posts list is empty</h3>
</template>

<script>
import PostItem from "@/components/PostItem";
export default {
  name: "PostList",
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
.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.3s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(150px)}

.post-list-move {
  transition: transform 0.8s ease;
}

</style>