<script>
import HeaderComponent from './Components/HeaderComponent.vue';
import MainComponent from './Components/MainComponent.vue';

export default {
  name: 'App',
  components: {
    HeaderComponent,
    MainComponent,
  },
};
</script>

<template>
  <HeaderComponent />
  <MainComponent />
</template>

<style scoped lang="scss">
header {
  height: 70px;
}
</style>
