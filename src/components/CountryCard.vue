<template>
  <div style="width: 18rem;" v-show="countryIsMatched" class="animated fadeIn">
    <img :src="countryObject.countryFlagLink" class="card-img-top" alt="flag" />
    <div class="card-body">
      <h5 class="card-title">{{ countryObject.countryName }}</h5>
      <p class="card-text">Capital: {{ countryObject.countryCapital }}</p>
      <p class="card-text">Country Region: {{ countryObject.countryRegion }}</p>
      <p class="card-text">SubRegion: {{ countryObject.countrySubRegion }}</p>
      <p class="card-text">Population: {{ countryObject.countryPopulation }}</p>
      <p class="card-text">Languages: {{ countryObject.countryLanguages }}</p>

      <p class="card-text">Currencies: {{ countryObject.countryCurrencies }}</p>
      <p class="card-text"></p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    countryObject: Object,
    countryIsMatched: Boolean
  }
};
</script>

<style></style>
