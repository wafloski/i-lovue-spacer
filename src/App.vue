<template>
  <div class="app">
    <div class="nav">
      <router-link to="/">home</router-link>
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
  .nav {
    position: fixed;
    height: 40px;
    background-color: rgba(0,0,0,0.5);
    color: #ddd;
    width: 100%;
    z-index: 1;
    display: flex;
    align-items: center;
    font-size: 14px;
    a {
      color: inherit;
      text-decoration: none;
      padding: 0 10px;
    }
  }
</style>
