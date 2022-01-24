<template>
  <div class="wrapper">
    <header class="header">
      <img class="header__logo" alt="beer-logo" src="./assets/logo.png">
      <h1 class="header__title">Hold your beer!</h1>
    </header>
    <section class="person">
      <Person />
    </section>
    <section class="beer">
      <Beer />
    </section>
  </div>
</template>

<style src="./assets/style.css"></style>

<script>
import Person from './components/Person.vue';
import Beer from './components/Beer.vue';

export default {
  name: 'App',
  components: {
    Person,
    Beer
  }
}
</script>