<script setup>
defineProps({
  msg: {
    type: String,
    required: true,
  },
})
</script>

<template>

  <div id="divComponente1">
    <h1>{{ msg }}</h1>
  </div>
</template>

<style scoped>
#divComponente1{
  background-color: rgb(78, 37, 97);
  margin:2%;
  color: white;
  text-align: center
}
</style>
