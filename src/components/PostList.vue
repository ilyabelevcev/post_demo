<template>
   <div class="post" v-for="post in posts" :key="post.id">
      <div><strong>Название:</strong> {{ post.title }} </div>
      <div><strong>Описание:</strong> {{ post.body }} </div>
   </div>
</template>

<script>
   export default {
      props: {
         posts: {
            type: Array,
            required: true,
         }
      }
   }
</script>

<style scoped>
   .post{
      margin: 10px 0px;
      padding: 15px;
      border: 2px solid teal;
   }
</style>