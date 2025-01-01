<template>
  <div class="container flex">
    <div class="flex">
      <img class="icon" :src="require(`@/assets/${iconSrc}`)" :alt="title + ' icon'"> 
      <span style="margin-left: 20px;">
        {{ title }}
      </span>
    </div>
    <span>
      {{ val }}
    </span>
  </div>
</template>

<script>
export default {
  name: 'InfoBox',
  props: {
    title: String,
    iconSrc: String,
    val: String
  }
}
</script>

<style scoped>
.container {
  padding: 10px 20px;
  justify-content: space-between;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}
</style>
