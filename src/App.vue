<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <div class="app__btns">
      <my-button @click.stop="showDialog">Создать пост</my-button>
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
  import MySelect from "@/components/UI/MySelect";

  export default {
    components: {
      MySelect,
      MyButton,
      MyDialog,
      PostForm, PostList
    },
    data() {
      return {
        posts: [],
        dialogVisible: false,
        isPostsLoading: false,
        selectedSort: '',
        sortOptions: [
          {value: 'title', name: 'По названию'},
          {value: 'body', name: 'По описанию'}
        ]
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
   },
    watch: {
      selectedSort(newValue) {

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

  .app__btns {
    margin: 15px 0;
    display: flex;
    justify-content: space-between;
  }


</style>