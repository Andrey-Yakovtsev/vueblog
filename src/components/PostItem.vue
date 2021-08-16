<template>
  <div class="post">
    <div>
    <div><strong>Название: </strong>{{post.title}}</div>
    <div><strong>Описание: </strong>{{post.body}}</div>
    </div>
      <div class="post__btns">
      <my-button
          @click="$emit('remove', post)"
      >Delete
      </my-button>
    </div>
  </div>

</template>

<script>
export default {
  name: "PostItem",
    props: {
    post: {
      type: Object,
      required: true
    }
  },
  methods: {
  }
}
</script>

<style scoped>
.post {
  margin-top: 15px;
  padding: 15px;
  border: 2px solid green;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

</style>