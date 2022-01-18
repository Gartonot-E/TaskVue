<template>
  <div class="alert-success">Товар был успешно добавлен</div>
</template>

<script>
export default {

}
</script>

<style scoped>
    .alert-success {
      position: fixed;
      top: 50px;
      right: 20px;
      z-index: 3;
      background: rgb(108 238 108 / 85%);
      padding: 16px 24px;
      border-radius: 4px;
      font-weight: 600;
      transition: .3s;
    }

    .fade-enter, 
    .fade-leave-to {
      opacity: 0;
    }
</style>