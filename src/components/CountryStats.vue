<template>
  <div class="container">
    <div class="row my-5">
      <div class="col-sm">
        <h2 class="text-center">Country Stats</h2>
        <p class="lead text-light">Choose a country to see stats</p>
      </div>
    </div>
    <div class="row">
      <div class="col-sm">
        <select @change="getCountry" class="form-control mb-5" :model="selectedCountry">
          <option v-for="country in countries" :key="country" :value="country">
            {{
            country
            }}
          </option>
        </select>
      </div>
    </div>
    <div v-if="selectedCountry" class="row">
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
  name: "CountryStats",
  data() {
    return {
      countries: [],
      selectedCountry: null,
      confirmed: null,
      deaths: null,
      recovered: null
    };
  },
  methods: {
    getCountry(e) {
      const countries = axios
        .get(`https://covid19.mathdro.id/api/countries/`)
        .then(response => {
          const selectedCountry = e.target.value;
          const countryCode = Object.entries(response.data.iso3);
          const countries = Object.entries(response.data.countries);

          countries.forEach(country => {
            if (country[0] === selectedCountry) {
              this.selectedCountryCode = country[1];
            }
          });

          countryCode.forEach(countryCode => {
            if (countryCode[0] === this.selectedCountryCode) {
              this.selectedCountry = countryCode[1];
            }
          });
          const stats = axios
            .get(
              `https://covid19.mathdro.id/api/countries/${this.selectedCountryCode}`
            )
            .then(response => {
              this.confirmed = response.data.confirmed.value;
              this.recovered = response.data.recovered.value;
              this.deaths = response.data.deaths.value;
            })
            .catch(error => {
              console.log(error);
            });
        })
        .catch(error => {
          console.log(error);
        });
    }
  },
  created() {
    axios.get("https://covid19.mathdro.id/api/countries/").then(response => {
      const countries = Object.keys(response.data.countries);
      countries.forEach(country => {
        this.countries.push(country);
      });
    });
  }
};
</script>

<style lang="scss">
</style>
