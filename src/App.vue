<template>

<div>
  <h1>Countries</h1>
  <div class="main-container">

    <countries-list :countries="countries"></countries-list>
    <country-detail :country="selectedCountry"></country-detail>

  </div>

</div>

</template>

<script>
import CountriesList from "./components/CountriesList.vue";
import CountryDetail from "./components/CountryDetail.vue";
import { eventBus } from "./main.js";

export default {
  name: 'app',
  data(){
    return {
    countries: [],
    selectedCountry: null
    };
  },
  mounted(){
    eventBus.$on("country-selected", (country) => {
      this.selectedCountry = country;
    });


    fetch("https://restcountries.eu/rest/v2/all")
    .then(data => data.json())
    .then(countries => this.countries = countries)
  },
  components: {
    "countries-list": CountriesList,
    "country-detail": CountryDetail
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
