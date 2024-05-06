<template>
  <header class="header">
      <nav class="header__nav">
          <router-link to="/projects" class="header__link" v-if="$route.name != 'projects'">Projects</router-link>
          <router-link to="/contacts" class="header__link" v-if="$route.name != 'contacts'">Contact</router-link>
          <router-link to="/" class="header__link" v-if="$route.name != 'home'">About me</router-link>
        </nav>
  </header>
</template>
