<template>
  <div class="app">
    <div class="nav">
      <router-link to="/">spacer</router-link>
      <router-link to="/about">about</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Roboto+Slab:300,400,700');

  * {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-family: 'Roboto Slab',sans-serif;
  }

  body {
    margin: 0;
    padding: 0;
    min-height: 100vh;
  }
</style>
