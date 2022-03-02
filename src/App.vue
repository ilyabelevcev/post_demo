<template> 
      <div class="app">
         <h1>Страница с постами</h1>
         <my-button @click="fetchPosts">
            Полчусить посты
         </my-button>
         <my-button 
            style="margin: 15px 0px;"
            @click="showDialog">
            Создать пост
         </my-button>
         <my-dialog  v-model:show="dialogVisible">
            <post-form
               @create="createPost"
            />
         </my-dialog>
         <post-list 
            :posts="posts"
            @remove="removePost"   
         />
      </div>
</template>

<script>
   import PostForm from '@/components/PostForm.vue';
   import PostList from '@/components/PostList.vue';
   import axios from 'axios'
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
            dialogVisible: false
         }
      },
      methods: {
         createPost(post) {
            this.posts.push(post);
            this.dialogVisible = false;
         },
         removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id);
         },
         showDialog() {
            this.dialogVisible = true;
         },
         async fetchPosts() {
            try {
               const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
               console.log(response)
            } catch (e) {
               alert('Ошибка')
            };
         }
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