<script>
import CardsList from './components/CardsList.vue';
export default {
  data() {
    return {

    }
  },
  components: {
    CardsList
  },

}
</script>



<template>
  <main class="container">
    <CardsList></CardsList>
  </main>
</template>


<style lang="scss">
@use './assets/scss/style.scss';

body {
  background-color: #D48F38;
}

main {
  background-color: white;
}
</style>