<template>
  <div id="app">
    <!-- HEADER -->
    <b-navbar toggleable="lg" type="dark" variant="primary">
      <b-navbar-brand href="#">LitoWEB</b-navbar-brand>
    </b-navbar>
    <!-- CONTENT CONTAINER -->
    <dashboard />
  </div>
</template>

<script>
import "./scss/custom-theme.scss";
import Dashboard from "./components/Dashboard.vue";

export default {
  name: "App",
  components: {
    Dashboard
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
