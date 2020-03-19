<template>
  <div id="app">
    <div class="row">
      <div class="col-sm">
        <h1 class="display-4 mt-5">Coronavirus Status Tracker</h1>
      </div>
    </div>
    <GlobalStats />
    <CountryStats />
    <Footer />
  </div>
</template>

<script>
import axios from "axios";
import GlobalStats from "./components/GlobalStats";
import CountryStats from "./components/CountryStats";
import Footer from "./components/Footer";

export default {
  name: "App",
  components: {
    GlobalStats,
    CountryStats,
    Footer
  },
  data() {
    return {};
  }
};
</script>

<style lang="scss">
$font-family: "Lato", sans-serif;

html {
  overflow-x: hidden;
}

body {
  background: #141e30; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #243b55,
    #141e30
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #243b55,
    #141e30
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

  padding: 0;
  margin: 0;
  font-family: $font-family;
}
#app {
  height: 100vh;
  text-align: center;
}

h1,
h2 {
  color: #f7f9f9;
}

.card {
  transition: 0.2s ease transform;

  @media screen and (max-width: 575px) {
    margin-bottom: 1.5rem;
  }
}

.card:hover {
  transform: scale(1.05);
}

h3 {
  font-size: 1.2rem;
}

p {
  color: #141e30;
  font-weight: bold;
  font-size: 1.6rem;
  margin-bottom: 0;
}
</style>
