<template>
  <div class="heroImage"/>
</template>

<script>
export default {
  name: "HeroImage"
};
</script>

<style lang="scss" scoped>
.heroImage {
  position: fixed;
  top: 0;
  z-index: -1;
  width: 100%;
  height: 100vh;
  background-image: url("../assets/bg.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 50% 0;
}
</style>

