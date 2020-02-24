<template>
  <div class="row justify-content-center">
    <ul class="list-group" v-show="matchedCountriesLen <= 5">
      <li
        @click="countrySelected(index)"
        class="list-group-item animated fadeIn"
        v-for="(country, index) in filteredList"
        :key="index"
      >
        {{ country.name }}
      </li>
    </ul>
    <hr />
    <transition leave-active-class="animated fadeOut">
      <country-card
        v-show="countryClicked"
        :countryObject="countryObject"
        :countryIsMatched="countryIsMatched"
      ></country-card>
    </transition>
  </div>
</template>

<script>
import { EventBus } from "../main.js";
import CountryCard from "./CountryCard.vue";

export default {
  components: {
    CountryCard
  },
  data() {
    return {
      countryData: [],
      countryList: [],
      countryObject: {
        countryName: "",
        countryCapital: "",
        countryRegion: "",
        countrySubRegion: "",
        countryPopulation: "",
        countryLanguages: [],
        countryCurrencies: [],
        countryFlagLink: ""
      },
      countrySearch: "",
      soloMatchSearch: "",
      countryIsMatched: false,
      matchedCountriesLen: 0,
      countryClicked: false
    };
  },
  methods: {
    countrySelected(index) {
      this.getCountryAtIndex(index, this.countryList, this.countryObject);
      this.countryClicked = true;
    },
    getCountryAtIndex(index, countryList, countryObject) {
      countryObject.countryName = countryList[index].name;
      countryObject.countryCapital = countryList[index].capital;
      countryObject.countryPopulation = countryList[index].population;
      countryObject.countryRegion = countryList[index].region;
      countryObject.countrySubRegion = countryList[index].subregion;
      countryObject.countryPopulation = countryList[index].population;
      countryObject.countryLanguages = countryList[index].languages[0].name;
      countryObject.countryCurrencies = countryList[index].currencies[0].code;
      countryObject.countryFlagLink = countryList[index].flag;
    }
  },
  computed: {
    filteredList() {
      //filter by country name
      return this.countryData.filter(country => {
        return country.name
          .toLowerCase()
          .includes(this.countrySearch.toLowerCase());
      });
    }
  },
  created() {
    EventBus.$on("country-data", data => {
      // console.log(this.countryData);
      this.countryData = data;
    });
    EventBus.$on("country-search", data => {
      this.countryClicked = false;
      this.countrySearch = data;
    });
  },
  updated() {
    //cause side effect
    let filtered = this.countryData.filter(country => {
      return country.name
        .toLowerCase()
        .includes(this.countrySearch.toLowerCase());
    });
    this.countryList = filtered;
    this.matchedCountriesLen = filtered.length;

    if (this.matchedCountriesLen === 1) {
      this.getCountryAtIndex(0, filtered, this.countryObject);

      this.countryIsMatched = true;
    } else if (this.matchedCountriesLen !== 1) {
      this.countryIsMatched = false;
    }
  }
};
</script>

<style></style>
