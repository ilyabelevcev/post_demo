<template>
   <button class="btn">
      <slot></slot>
   </button>
</template>

<script>
   export default {
      name: 'my-button',
   }
</script>

<style scoped>
   .btn{
      background-color: #fff;
      color: teal;
      font-weight: 500;
      border: 2px solid teal;
      border-radius: 10px;
      padding: 5px 20px;
      cursor: pointer;
   }
</style>