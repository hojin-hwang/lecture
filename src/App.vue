<script setup>
import { RouterLink, RouterView } from 'vue-router'
import consoleLog from './assets/js/console-log.js'

consoleLog('new Text');

const jQuery = 7;

(($) => {
    //$ 사용가능
})(jQuery);

</script>

<template>
  <header>
    <div class="wrapper">
      <nav>
        <RouterLink to="/rule">Rule</RouterLink>
        <RouterLink to="/function">Function</RouterLink>
        <RouterLink to="/jquery">jQuery</RouterLink>
      </nav>
    </div>
  </header>
  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  display: flex;
  flex-direction: row;
  width: 100%;
  font-size: 12px;
  text-align: center;
}

nav a.router-link-exact-active {
  /* color: var(--color-text); */
  color: hsla(160, 100%, 37%, 1);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    
    /* place-items: center; */
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;
    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
