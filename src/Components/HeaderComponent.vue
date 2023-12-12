<script>
export default {
  name: 'HeaderComponent',
};
</script>

<template>
  <header>
    <img src="../assets/img/logo.png" alt="logo" />
    <h1>Yu-Gi-Oh Api</h1>
  </header>
</template>

<style scoped lang="scss">
header {
  display: flex;
  align-items: center;
  background-color: #fff;
  img {
    width: 50px;
    margin: 0 26px;
  }
}
</style>
