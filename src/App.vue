<script setup>
import RegistrationForm from './components/RegistrationForm.vue'
</script>

<template>
  <header>
    <img alt="Lorem Ipsum logo" class="logo" src="./assets/logo-min.svg" width="125" height="125" />
  </header>

  <main>
    <RegistrationForm />
  </main>
</template>

<style scoped>
.logo {
  display: block;
  margin: 0 auto 2vh;
}
</style>

<style>
@media (min-width: 1024px) {
    #app {
      grid-template-columns: 1fr !important;
    }
}
</style>
