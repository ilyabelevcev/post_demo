<template> 
      <div class="app">
         <h1>Страница с постами</h1>
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
            v-if="isPostLoading !== true"   
         />
         <div v-else>Идёт загрузка...</div>
         <div class="page__wrapper">
            <div
               v-for="pageNumber in totalPages"
               class="page"
               :key="pageNumber"
               :class="{'current-page': page === pageNumber}"
               @click="changePage(pageNumber)">
               {{ pageNumber }}
            </div>
         </div>
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
            posts: [],
            dialogVisible: false,
            isPostLoading: false,
            page: 1,
            limit: 15,
            totalPages: 0,
         }
      },
      methods: {
         createPost(post) {
            this.posts.unshift(post);
            this.dialogVisible = false;
         },
         removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id);
         },
         showDialog() {
            this.dialogVisible = true;
         },
         changePage(pageNumber) {
            this.page = pageNumber;
         },
         async fetchPosts() {
            try {
               this.isPostLoading = true;
               const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                  params: {
                     _page: this.page,
                     _limit: this.limit,
                  }
               });
               this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
               this.posts = response.data;
            } catch (e) {
               alert('Ошибка')
            } finally {
               this.isPostLoading = false;
            }
         },
      },
      mounted() {
         this.fetchPosts();
      },
      watch: {
         page() {
            this.fetchPosts()
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
   .page__wrapper{
      display: flex;
      margin-top: 10px;
   }
   .page{
      border: 1px solid #000;
      padding: 10px;
   }
   .current-page{
      border: 2px solid teal;
   }
</style>