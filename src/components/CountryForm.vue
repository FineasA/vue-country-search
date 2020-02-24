<template>
  <div class="row justify-content-center animated fadeIn">
    <form v-on:submit.prevent="countryGet">
      <div class="form-group">
        <label for="countrySearch">Search for a country...</label>
        <input
          type="text"
          class="form-control"
          id="countrySearch"
          v-model="countrySearch"
        />
      </div>
    </form>
  </div>
</template>

<script>
import { EventBus } from "../main.js";

export default {
  data() {
    return {
      countrySearch: "",
      countryData: []
    };
  },
  methods: {
    getCountryData() {
      this.$http.get(`https://restcountries.eu/rest/v2/all`).then(response => {
        // console.log(response);
        this.countryData = response.data;
        EventBus.$emit("country-data", this.countryData);
      });
    }
  },
  created() {
    this.getCountryData();
  },
  updated() {
    EventBus.$emit("country-search", this.countrySearch);
  }
};
</script>

<style></style>