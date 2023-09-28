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

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Open+Sans&family=Roboto+Condensed&display=swap');

  :root {
    --font-family-base: 'Open Sans', 'Arial', sans-serif;
    --font-family-accent: 'Work Sans', 'Arial', sans-serif;
    --font-size-base: 16px;
  }

  html {
    font-size: var(--font-size-base);
  }

  html,
  body {
    background-color: #fff;
    font-family: var(--font-family-base);
  }

  a {
    text-decoration: none;
    color: #1c75bc;
    transition: all 0.3s cubic-bezier(0.25, 0.45, 0.45, 0.95);
  }

  @media (hover: hover) {
    a:hover {
      text-decoration: underline;
    }
  }
</style>
