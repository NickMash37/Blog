<template>
  <div>
    <h1>Страница с постами</h1>
    <my-button @click.stop="showDialog" style="margin: 15px 0">Создать пост</my-button>
    <my-dialog v-model:show="dialogVisible">
      <post-form
          @create="createPost"
      />
    </my-dialog>

    <post-list
        :posts="posts"
        @remove="removePost"
        v-if="!isPostsLoading"
    />
    <div v-else style="font-size: 20px; width: 100%">Идет загрузка...</div>
  </div>
</template>

<script>
  import PostList from '@/components/PostList.vue'
  import PostForm from '@/components/PostForm'
  import MyDialog from "@/components/UI/MyDialog";
  import MyButton from "@/components/UI/MyButton";
  import axios from 'axios';

  export default {
    components: {
      MyButton,
      MyDialog,
      PostForm, PostList
    },
    data() {
      return {
        posts: [],
        dialogVisible: false,
        isPostsLoading: false
      }
    },

    methods: {
      createPost(post) {
        this.posts.push(post)
        this.dialogVisible = false
      },

      removePost(post) {
        this.posts = this.posts.filter(p => p.id !== post.id)
      },

      showDialog() {
        this.dialogVisible = true
      },

      async fetchPosts() {
        try {
          this.isPostsLoading = true
          setTimeout(async () => {
            const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
            this.posts = response.data;
            this.isPostsLoading = false;
          }, 1000)
        } catch (e){
          alert('Ошибка!')
        }
      }
    },
    mounted() {
      this.fetchPosts();
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