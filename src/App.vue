<template> 
      <div class="app">
         <post-form @create="createPost"/>
         <post-list :posts="posts"/>
      </div>
</template>

<script>
   import PostForm from '@/components/PostForm.vue';
   import PostList from '@/components/PostList.vue';
   export default {
      components: {
         PostForm,
         PostList,
      },
      data() {
         return {
            posts: [
               {id: 0, title: 'Vue.js 1', body: 'Описание поста 1'},
               {id: 1, title: 'Vue.js 2', body: 'Описание поста 2'},
               {id: 2, title: 'Vue.js 3', body: 'Описание поста 3'},
            ],
         }
      },
      methods: {
         createPost(post) {
            this.posts.push(post);
         },
      }
   }
</script>

<style>
   *{
      box-sizing: border-box;
      margin: 0;
      padding: 0;
   }

   .app{
      padding: 20px;
   }

   .title{
      text-align: center;
      font-size: 50px;
   }
</style>