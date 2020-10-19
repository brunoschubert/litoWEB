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
    Dashboard,
  },
};
</script>

<style>
@font-face {
  font-family: "Montserrat";
  src: local("Montserrat"),
    url(./fonts/Montserrat-Regular.ttf) format("truetype");
}
#app {
  font-family: "Montserrat", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  height: 100vh;
  background-color: #4e5050;
}
.navbar-brand {
  font-family: "Montserrat";
  font-size: 25px;
  font-weight: 500;
}
</style>
