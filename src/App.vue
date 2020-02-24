<template>
  <div class="container">
    <h3 class="appTitle">
      Country Information
    </h3>
    <hr />
    <country-form></country-form>
    <hr />
    <country-search></country-search>
  </div>
</template>

<script>
import CountryForm from "./components/CountryForm.vue";
import CountrySearch from "./components/CountrySearch.vue";

export default {
  components: {
    CountryForm,
    CountrySearch
  }
};
</script>

<style>
.appTitle {
  text-align: center;
}
</style>
