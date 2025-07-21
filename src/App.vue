<template>
  <nav class="navbar is-light" role="navigation" aria-label="main navigation">
    <div class="container">
      <div class="navbar-brand">
        <router-link to="/" class="navbar-item has-text-weight-bold is-size-4">
          <img alt="Vue logo" :src="logo" />
          Vue.js
        </router-link>

        <a role="button" class="navbar-burger" :class="{ 'is-active': isActive }" aria-label="menu"
          aria-expanded="false" @click="toggleMenu">
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <div :class="['navbar-menu', { 'is-active': isActive }]">
        <div class="navbar-end">
          <router-link to="/" class="navbar-item" @click="closeMenu">Inicio</router-link>
          <router-link to="/contacts" class="navbar-item" @click="closeMenu">Contactos</router-link>
          <router-link to="/about" class="navbar-item" @click="closeMenu">Acerca de</router-link>
        </div>
      </div>
    </div>
  </nav>
  <section class="section">
    <div class="container">
      <router-view />
    </div>
  </section>
</template>

<script>
import logo from './assets/logo.png';

export default {
  name: 'Header',
  data() {
    return {
      isActive: false,
      logo
    }
  },
  methods: {
    toggleMenu() {
      this.isActive = !this.isActive;
    },
    closeMenu() {
      this.isActive = false;
    },
  },
}
</script>
<style scoped>
.navbar .navbar-item:hover {
  background-color: transparent !important;
}
</style>