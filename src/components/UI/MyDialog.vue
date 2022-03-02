<template>
   <div class="dialog" v-if="show === true" @click.stop="hideDialog">
      <div @click.stop class="dialog__content">
         <slot></slot>
      </div>
   </div>
</template>

<script>
   export default {
      name: 'my-dialog',
      props: {
         show: {
            type: Boolean,
            default: false,
         }
      },
      methods: {
         hideDialog() {
            this.$emit('update:show', false)
         }
      }
   }
</script>

<style scoped>
   .dialog{
      position: fixed;
      top: 0;
      bottom: 0;
      left: 0;
      right: 0;
      background: rgba(0, 0, 0, 0.5);
      display: flex;
   }
   .dialog__content{
      margin: auto;
      background-color: #fff;
      border-radius: 15px;
      min-height: 60px;
      min-width: 500px;
      padding: 15px;
   }
</style>