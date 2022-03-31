<template>
  <div v-show="posts.length > 0">
    <h3>Текущие записи</h3>
    <post-item
        v-for="post in posts"
        :post="post"
        :key="post.id"
        @remove="$emit('remove', post)"/>
  </div>
  <h2 v-show="posts.length === 0" style="color: dimgrey; font-size: 30px; font-weight: 700;">А здесь ничего нет :(</h2>
</template>

<script>
  import PostItem from "@/components/PostItem";
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

</style>