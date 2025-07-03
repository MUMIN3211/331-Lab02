<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'

</script>

<template>
 <div id="layout">
  <header>
    <div class="wrapper">
      <nav>
          <RouterLink to="/">Event</RouterLink>
          <span class="nav-separator">|</span>
          <RouterLink to="/about">About</RouterLink>
          <span class="nav-separator">|</span>
          <RouterLink to="/students">Student</RouterLink>
      </nav>
    </div>
  </header>
    <RouterView />
  </div>
</template>

<style>
#layout {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
 
}

h2 {
  font-size: 20px;
}

nav {
  padding: 30px;
}

nav a {
  color: #2c3e50;
  text-decoration: none;
  margin: 0 5px;
  transition: color 0.2s;
}

nav a:hover {
  color: #005a3c;
}

.nav-separator {
  margin: 0 8px;
  color: #888;
}

nav a.router-link-exact-active {
  color: #42b983;
  text-decoration: underline;
}
</style>
