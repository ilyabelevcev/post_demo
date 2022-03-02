<template>
   <div v-if="posts.length > 0">
      <h3>Список постов</h3>
      <post-item 
         v-for="post in posts" :key="post.id"
         :post="post"
         @remove="$emit('remove', post)"
      />
   </div>
   <h2 v-else style="text-align: center; font-size: 40px;">Пусто</h2>
</template>

<script>
   import PostItem from '@/components/PostItem.vue'
   export default {
      components: {
         PostItem
      },
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