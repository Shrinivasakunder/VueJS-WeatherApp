<template>
  <div class="container">
    {{ message }}
  </div>
</template>

<script>
export default {
  name: 'ErrorPopup',
  props: {
    message: String
  }
}
</script>

<style scoped>
.container {
  position: absolute;
  top: 10%;
  padding: 30px;
  background-color: #ad424b;
  border-radius: 15px;
}
</style>
