<template>
   <div>
      <form class="form" @submit.prevent>
         <h2>Создание поста</h2>
         <my-input
            v-model="post.title"
            type="text" 
            placeholder="Название поста"
         />

         <my-input 
            v-model="post.body"
            type="text" 
            placeholder="Описание поста"
         />

         <my-button 
            class="btn" 
            @click="createPost"
            style="margin-top: 10px; align-self: flex-end;">
            Создать
         </my-button>
      </form>
   </div>
</template>

<script>
   export default {
      data() {
         return {
            post: {
               title: '',
               body: '',
            }
         }
      },
      methods: {
         createPost() {
            this.post.id = Date.now();
            this.$emit('create', this.post)
            this.post = {
               title: '',
               body: '',
            }
         },
      }
   }
</script>

<style scoped>
   .form{
      display: flex;
      flex-direction: column;
   }
</style>