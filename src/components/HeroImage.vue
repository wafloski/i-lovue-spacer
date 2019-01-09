<template>
  <div class="hero-image"></div>
</template>

<script>
export default {
  name: 'HeroImage',
};
</script>

<style lang="scss" scoped>
  .hero-image {
    position: fixed;
    top: 0;
    z-index: -1;
    width: 100%;
    height: 100%;
    background-image: url('../assets/herospacer.jpg');
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center center;

    &::after {
      content: '';
      background: rgba(0,0,0,.05);
      position: absolute;
      top: 0;
      left: 0;
      z-index: 1;
      width: 100%;
      height: 100%;
    }
  }
</style>
