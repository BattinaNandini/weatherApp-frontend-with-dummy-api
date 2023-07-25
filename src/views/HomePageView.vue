<template>
  <div class="homePageView" :id="weatherNow">
    <br />

    <input
      type="text"
      placeholder="search..."
      v-model="enteredSearch"
      @keypress.enter="ChangeSearch"
    />
    <img id="img_" src="../assets/loupe.png" @click="ChangeSearch" />
    <p>{{ noSearch }}</p>
    <br />
    <br />
    <br />
    <br />
    <div v-if="searchedLocation.length > 0 && current.length!=0">
      <HomePageComponent
        :currentData="current"
        :locationData="location"
        :hourData="hour"
      ></HomePageComponent>
      <ForeCastComponent
        :astronomyData="astronomy"
        :forecastData="forecast"
        :currentData="current"
      ></ForeCastComponent>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import VueFullscreen from "vue-fullscreen";
import Vue from "vue";
Vue.use(VueFullscreen);
import HomePageComponent from "@/components/HomePageComponent.vue";
import ForeCastComponent from "@/components/ForeCastComponent.vue";
export default {
  name: "HomePageView",
  components: {
    HomePageComponent,
    ForeCastComponent,
  },
  data() {
    return {
      astronomy: [],
      hour: [],
      location: [],
      current: [],
      forecast: [],
      weatherNow: "",
      searchedLocation: "",
      enteredSearch: "",
      noSearch:"",
    };
  },

  /* eslint-disable */
  methods: {
    ChangeSearch() {
      if (this.enteredSearch.length > 0) {
        this.searchedLocation = this.enteredSearch;


        let weatherAPI =
          "http://api.weatherapi.com/v1/forecast.json?key=cf55f70d42274f91b3771517230802&q=" +
          this.searchedLocation +
          "&days=20";

        axios
          .get(weatherAPI)
          .then((result) => {
            console.log(result);

            if (result.status !== 400) {
              this.current = result.data.current;
              this.location = result.data.location;
              this.forecast = result.data.forecast.forecastday;
              this.hour = this.forecast[0].hour;
              this.astronomy = this.forecast[0].astro;

              this.forecast = this.forecast.slice(1);

              console.log(this.forecast);

              let timeNow = this.location.localtime.split(" ");
              timeNow = timeNow[1].split(":")[0];

              this.hour = this.hour.slice(timeNow);
              this.hour = this.hour.slice(1);
              console.log(this.hour);

              this.weatherNow = this.current.condition?.text;

              this.weatherNow = this.weatherNow
                .toLocaleLowerCase()
                .split(" ")
                .join("");
            } else {
              console.log("Not found");
            }
          })
          .catch((error) => {
              this.noSearch="City not Found"
              console.log(error.response.status);
              this.astronomy = [];
              this.hour = [];
              this.location = [];
              this.current = [];
              this.forecast = [];
              this.weatherNow = "";
              this.searchedLocation = "";
              this.enteredSearch = "";
            
          });
      }
    },
  },
};
</script>
