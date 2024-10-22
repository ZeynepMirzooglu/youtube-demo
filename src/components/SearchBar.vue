<template>
  <div>
    <form @submit.prevent="handleSubmit">
        <input type="text" v-model="searchTerm" >
        <button>Ara</button>
    </form>
  </div>
</template>

<script>
export default {
  emits:['termChange'],
data() {
  return {
    searchTerm:''
  }
},
methods: {
  handleSubmit(){
    this.$emit('termChange',this.searchTerm);
    this.searchTerm=''
  }
},
}
</script>

<style>

</style>