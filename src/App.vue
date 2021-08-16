<template>
  <div class="app">
    <h1>Posts Pages</h1>
    <my-input
        v-model="searchQuery"
        placeholder="Search..."
    ></my-input>
    <div class="app__buttons">
      <my-button
          @click="showDialog"
      >
        Create new post
      </my-button>
      <my-select
          v-model="selectedSort"
          :options="sortOptions"
      ></my-select>
    </div>

    <my-dialog v-model:show="dialogVisible">
      <post-form
          @create="createPost"
      />
    </my-dialog>

    <post-list
        :posts="filteredPosts"
        @remove="removePost"
    />
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import MyDialog from "@/components/UI/MyDialog";
import MyButton from "@/components/UI/MyButton";
import axios from 'axios'
import MySelect from "@/components/UI/MySelect";
import MyInput from "@/components/UI/MyInput";
export default {
  name: "App",
  components: {
    MyInput,
    MySelect,
    MyButton,
    MyDialog,
    PostList,
    PostForm
  },

  data: ()=> ({
    posts: [
      {id: 1, title: 'Title 1', body:'Body 1'},
      {id: 2, title: 'Title 2', body:'Body 2'},
      {id: 3, title: 'Title 3', body:'Body 3'}
    ],
    dialogVisible: false,
    selectedSort: '',
    searchQuery: '',
    sortOptions: [
      {value: 'title', name: 'By title'},
      {value: 'body', name: 'By body'}
    ]
  }),

  methods: {
    createPost (post) {
      this.posts.push(post)
      this.dialogVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showDialog() {
      this.dialogVisible = true;
    },
    async fetchPosts () {
      try {
        const response = await axios.get(
            'https://jsonplaceholder.typicode.com/posts?_limit=10');
        this.posts = response.data
      } catch (e) {
        alert('Error')
      }},
  },
  mounted() {
    this.fetchPosts();
  },
  computed: {
    filteredPosts () {
      return this.posts.filter(post => post.title.includes(this.searchQuery))
    },
  },
  watch: {
    selectedSort(newValue) {
      this.posts.sort((post1, post2) => {
        return post1[newValue]?.localeCompare(post2[newValue])
      })
    }
  },
}
</script>

<style>
* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;

}
.app {
  padding: 20px;
}
.app__buttons {
  display: flex;
  justify-content: space-between;
  margin: 15px 0px
}

</style>