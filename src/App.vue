<template>
  <div class="app">
    <post-form
        @create="createPost"
    />
    <post-list
        :posts="posts"
    />
  </div>
</template>

<script>
  import PostList from '@/components/PostList.vue'
  import PostForm from '@/components/PostForm'

  export default {
    components: {
      PostForm, PostList
    },
    data() {
      return {
        posts: [
          {id: 1, title: 'JavaScript', body: 'Just a text'},
          {id: 2, title: 'TypeScript', body: 'Type your text here'},
          {id: 3, title: 'Vue.JS', body: 'Could it work?'},
        ],
      }
    },

    methods: {
      createPost(post) {

      }
    }
  }

</script>

<style>

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    max-width: 100%;
  }

  .app {
    padding: 20px;
  }


</style>