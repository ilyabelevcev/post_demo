<template>
   <div>
      <form class="form" @submit.prevent>
         <h2>Создание поста</h2>
         <input
            v-model="post.title"
            class="input" 
            type="text" 
            placeholder="Название поста"
         >

         <input 
            v-model="post.body"
            class="input"
            type="text" 
            placeholder="Описание поста"
         >

         <button class="btn" @click="createPost">Создать</button>
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

   .input{
      width: 100%;
      margin-top: 15px;
      padding: 10px 15px;
      border: 1px solid teal;
   }

   .btn{
      margin-top: 10px;
      background-color: #fff;
      color: teal;
      font-weight: 500;
      border: 2px solid teal;
      border-radius: 10px;
      padding: 5px 20px;
      cursor: pointer;
      align-self: flex-end;
   }
</style>