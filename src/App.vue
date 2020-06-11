<template>
  <div id="app">
    <navbar />
    <div class="container">
      <router-view />
    </div>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar';
export default {
  components: {
    'navbar' : Navbar,
  }
}
</script>

<style lang="scss">
  @import "~materialize-css/dist/css/materialize.min.css";
</style>
