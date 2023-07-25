<template>
  <div id="app">
    <!-- <nav>
      <router-link to="/">User</router-link>  |
      <router-link to="/admin">Admin</router-link> 
    </nav> -->
    <router-view/>
  </div>
</template>

<style>


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
}

/* nav {
  padding: 20px;

}

nav a {
  font-weight: bold;
  color: #000;
}

nav a.router-link-exact-active {
  color: #03f217;
} */
</style>
