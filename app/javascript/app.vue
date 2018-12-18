<template>
  <div id="app">
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
    props: ["original_lists"],

}
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: center;
}
</style>
