<script>
export default {
  name: 'CardComponent',
  props: ['img', 'name', 'archetype'],
};
</script>

<template>
  <div class="img">
    <img :src="img" :alt="name" />
  </div>
  <div class="text">
    <div class="caption">{{ name }}</div>
    <div class="description">{{ archetype }}</div>
  </div>
</template>

<style scoped lang="scss">
@use '../assets/scss/partial/variables' as *;

.text {
  background-color: $primary-color;
  flex-grow: 1;
}
.caption,
.description {
  padding-top: 25px;
  color: #fff;
  text-transform: uppercase;
  text-align: center;
}
.description {
  color: #000;
  text-transform: none;
  padding-bottom: 6px;
}
</style>
