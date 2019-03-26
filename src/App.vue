<template>
  <div class="app">
    <div class="nav">
      <router-link to="/">spacer</router-link>
      <router-link to="/about">about</router-link>
    </div>
    <router-view />
  </div>
</template>

<style scoped lang="scss">
  body {
    margin: 0;
  }
</style>
