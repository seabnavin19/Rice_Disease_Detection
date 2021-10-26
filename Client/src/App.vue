<template>
 <nav class="navbar navbar-light bg-success">
  <a class="navbar-brand" href="#">
    <img src="./assets/logo.jpg" width="30" height="30" class="d-inline-block align-top" alt="">
    Doctor Srov
  </a>
</nav>
  <router-view />
  
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
