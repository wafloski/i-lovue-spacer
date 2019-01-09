<template>
  <div class="about">
    <h1 class="title">A brief summary of the work done in this application</h1>
    <p>Technologies stack:</p>
    <ul>
      <li>VueJS</li>
      <li>ES6</li>
      <li>HTML</li>
      <li>SCSS</li>
    </ul>
    <p>Tools:</p>
    <ul>
      <li>lodash</li>
      <li>axios</li>
      <li>eslint</li>
      <li>github</li>
      <li>ide: phpstorm</li>
    </ul>
    <p>Content is taken from NASA API</p>
  </div>
</template>

<script>
export default {
  name: 'About',
};
</script>

<style lang="scss" scoped>
  .about {
    padding: 30px;
    .title {
      font-size: 24px;
    }
  }
</style>
