<script>
export default {
  name: 'LoaderComponent',
};
</script>

<template>
  <div class="container">
    <div class="loader">Caricamento in corso...</div>
  </div>
</template>

<style scoped lang="scss">
@use '../assets/scss/partial/variables' as *;
.container {
  background-color: #fff;
  max-width: 1180px;
  margin: 0 auto;
  padding: 48px;
  text-align: center;
}
</style>
