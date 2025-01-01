<template>
  <div class="wrapper container flex">
    <input type="text" list="list" v-model="val" :placeholder="placeholder">
    <datalist id="list">
      <option v-for="(data, i) in dataList" :value="data" :key="i" />
    </datalist>
    <button @click="search(val), val = ''">{{ buttonValue }}</button>  
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  data() {
    return {
      val: ''
    }
  },
  props: {
    placeholder: String,
    buttonValue: String,
    dataList: Array
  },
  methods: {
    search(val) {
      this.$emit('onSearch', val);
    }
  }

}
</script>

<style scoped>
.container {
  background-color: rgba(0, 0, 0, 0.7);
  border-bottom-left-radius: 15px; 
  border-bottom-right-radius: 15px;
}
</style>
