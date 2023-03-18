<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="wrapper">
      <nav>
        <h1 class="logo">Shiley</h1>
        <div class='menu'>
          <RouterLink to="/">Home</RouterLink>
          <RouterLink to="/repos">Repos</RouterLink>
        </div>

      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.2;
  max-height: 100vh;
  background: #fff;
  padding: 0 24px;
}

.logo {
  font-size: 28px;
  font-family: 'Satisfy', cursive;
}

nav {
  width: 100%;
  font-size: 16px;
  text-align: center;
  padding-top: 1rem;
  padding-bottom: 1rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

nav a.router-link-exact-active {
  color: #d5a419;
}

.menu {
  display: flex;
  gap: 24px;
}

.menu > * {
  position: relative;
}

.menu > *::after {
  content: "";
  position: absolute;
  width: 100%;
  height: 1px;
  background-color: currentColor;
  width: 100%;
  bottom: -2px;
  left: 0;
  right: 0;
  transform: scaleX(0);
  border-radius: 0.5rem;
  transform-origin: right;
  transition: transform 250ms ease;
}

.menu > *:hover::after,
.menu > *:focus::after {
  transform: scaleX(1);
  transform-origin: left;
  outline: none;
}

@media screen and (min-width: 800px) {
  header {
    padding: 0 48px;
  }
}

</style>
