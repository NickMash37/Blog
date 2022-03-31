<template>
  <div class="header">
    <div class="post">
      <div><strong>Название:</strong> Пост о Javascript</div>
      <div><strong>Описание:</strong> JS - универсальный язык программирования</div>
    </div>
    <div class="post">
      <div><strong>Название:</strong> Пост о Javascript</div>
      <div><strong>Описание:</strong> JS - универсальный язык программирования</div>
    </div>
    <div class="post">
      <div><strong>Название:</strong> Пост о Javascript</div>
      <div><strong>Описание:</strong> JS - универсальный язык программирования</div>
    </div>
  </div>

</template>

<script>
  export default {
    data() {
      return {
        likes: 0,
        dislikes: 0,
      }
    },

    methods: {
      addLike() {
        this.likes += 1
      },

      addDislike() {
        this.dislikes += 1
      }
    }
  }

</script>

<style>

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .post {
    padding: 15px;
    border: 1px solid teal;
  }

</style>