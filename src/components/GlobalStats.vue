<template>
  <div class="container">
    <div class="row">
      <div class="col-sm">
        <h2 class="my-5 text-center">Global Stats</h2>
      </div>
    </div>
    <div class="row">
      <div class="col-sm">
        <div class="card">
          <div class="card-body">
            <h3 class="text-secondary">Cases</h3>
            <p>{{ confirmed }}</p>
          </div>
        </div>
      </div>
      <div class="col-sm">
        <div class="card">
          <div class="card-body">
            <h3 class="text-secondary">Recovered</h3>
            <p>{{ recovered }}</p>
          </div>
        </div>
      </div>
      <div class="col-sm">
        <div class="card">
          <div class="card-body">
            <h3 class="text-secondary">Deaths</h3>
            <p>{{ deaths }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Global",
  data() {
    return {
      confirmed: null,
      recovered: null,
      deaths: null
    };
  },
  created() {
    axios.get("https://covid19.mathdro.id/api/").then(response => {
      this.confirmed = response.data.confirmed.value;
      this.recovered = response.data.recovered.value;
      this.deaths = response.data.deaths.value;
    });
  }
};
</script>

<style>
</style>