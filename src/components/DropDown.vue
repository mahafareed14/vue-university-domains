<template>
  <v-container align="center">
    <div class="resize">
      <v-row align="center">
        <div class="text-h6 mb-1">Select a Country:</div>
        <v-col class="d-flex" cols="12" sm="6">
          <v-select
            :items="country"
            filled
            v-model="selectedCountry"
            label="Select Country"
            dense
          ></v-select>
        </v-col>
      </v-row>
      <v-row align="center" v-if="selectedCountry.length">
        <div class="text-h6 mb-1">Select a University:</div>
        <v-col class="d-flex" cols="12" sm="6">
          <v-select
            :items="university"
            filled
            v-model="selectedUniverity"
            label="Select University"
            dense
          ></v-select>
        </v-col>
      </v-row>
    </div>
    <DomainDetails
      v-if="domains.length && web_pages.length"
      :domains="domains"
      :webpages="web_pages"
    ></DomainDetails>
  </v-container>
</template>
<script>
import axios from "axios";
import DomainDetails from "./DomainDetails.vue";
const API_URL =
  "https://raw.githubusercontent.com/Hipo/university-domains-list/master/world_universities_and_domains.json";

export default {
  name: "DropDown",
  data: () => ({
    country: [],
    university: [],
    selectedCountry: "",
    selectedUniverity: "",
    universityMap: [],
    web_pages: [],
    domains: [],
  }),
  components: {
    DomainDetails,
  },
  created() {
    this.country = [];
    this.getAllData().then((data) => {
      this.country = this.getAllCountries(data);
      this.universityMap = this.mapUniversitirestoCountry(data);
    });
  },
  watch: {
    selectedCountry(newCountry) {
      this.selectedUniverity = "";
      this.domains = [];
      this.web_pages = [];
      if (newCountry.length) this.getUniversityofSelectedCountry(newCountry);
    },
    selectedUniverity(newUniversity) {
      if (newUniversity.length) this.getDomainsandWebPages(newUniversity);
    },
  },
  methods: {
    async getAllData() {
      const response = await axios.get(API_URL);
      return response.data;
    },

    mapUniversitirestoCountry(data) {
      let arr = [];
      for (let i = 0; i < this.country.length; i++) {
        const x = data.filter((data) => data.country === this.country[i]);
        let obj = {
          name: this.country[i],
          university: x,
        };
        arr.push(obj);
      }
      return arr;
    },

    getAllCountries(data) {
      let duplicateCountries = data.map((obj) => obj.country);
      let allCountries = duplicateCountries
        .filter((c, index) => duplicateCountries.indexOf(c) == index)
        .sort();
      return allCountries;
    },
    getUniversityofSelectedCountry(newCountry) {
      let alldata = this.universityMap.filter((obj) => obj.name == newCountry);
      let obj_university = alldata[0].university;
      this.university = obj_university.map((obj) => obj.name).sort();
    },
    getDomainsandWebPages() {
      if (this.selectedUniverity.length && this.selectedCountry.length) {
        let alldata = this.universityMap.filter(
          (obj) => obj.name == this.selectedCountry
        );
        let arr = alldata[0].university.filter(
          (obj) => obj.name == this.selectedUniverity
        );
        console.log(arr[0].domains);
        console.log(arr[0].web_pages);
        this.domains = arr[0].domains;
        this.web_pages = arr[0].web_pages;
      }
    },
  },
};
</script>
<style>
.resize {
  width: 70%;
}
</style>
