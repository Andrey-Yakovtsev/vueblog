<template>
  <div>
    <h4>Create post</h4>
    <form @submit.prevent>
      <my-input
          v-model:value="post.title"
          type="text"
          placeholder="Title"/>
      <my-input
          v-model:value="post.body"
          type="text"
          placeholder="Body"/>
      <my-button class="btn" style="align-self: flex-end" @click="createPost">Create</my-button>
    </form>

  </div>
</template>

<script>
export default {
  name: "PostForm",
  data: () => ({
    post: {
      title: '',
      body: ''
    }
  }),
  methods: {
    createPost() {
      this.post.id = Date.now()
      this.$emit('create', this.post)
      this.post = {
        title: '',
        body: ''
      }
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}


.btn{
  margin-top: 15px;
}

</style>