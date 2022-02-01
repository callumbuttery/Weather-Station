<template>
  <v-container>
    <v-row class="text-center" no-gutters>
      <v-col>
        <v-skeleton-loader class="mx-auto" max-width="500" type="card">
          <v-card color="purple darken-3" elevation="14" height="400px">
            <v-card-title
              class="text-h4 white--text purple darken-1 justify-center"
              >Current Weather</v-card-title
            >
            <v-card-title
              class="text-h5 white--text purple darken-1 justify-center"
              >{{ this.currentLocation }}</v-card-title
            >
            <v-img
              class="mx-auto"
              :src="this.currentWeatherImg"
              max-height="125"
              max-width="125"
            ></v-img>
            <v-card-subtitle
              class="text-h5 white--text purple darken-1 justify-center"
              >{{
                this.rawApiData.temp_c +
                "C" +
                " / " +
                this.rawApiData.temp_f +
                "F"
              }}</v-card-subtitle
            >
            <v-btn color="white" class="mt-5" @click="overlay = !overlay">
              Details
            </v-btn>
            <v-overlay :absolute="absolute" :value="overlay" color="black">
              <v-card class="purple darken-3">
                <v-btn color="purple" @click="overlay = false">
                  Hide Details
                </v-btn></v-card
              ></v-overlay
            >
          </v-card>
        </v-skeleton-loader>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "CurrentWeather",
  props: {
    search: String,
  },
  data() {
    return {
      rawApiData: "",
      currentLocation: "",
      currentWeatherImg: "",
      absolute: true,
      overlay: false,
      locationToSearch: "Glasgow",
    };
  },
  methods: {
    breakdownApi: function (apiData) {
      this.rawApiData = apiData.data.current;
      this.currentLocation = apiData.data.location.name;
      this.currentWeatherImg = apiData.data.current.condition.icon;
    },
    callApi: async function () {
      console.log(this.$props.search);
      await axios
        .get(
          `https://api.weatherapi.com/v1/current.json?key=${
            process.env.VUE_APP_WEATHER_API_KEY
          }&q=${this.$props.search || this.locationToSearch}&aqi=yes`
        )
        .then((response) => this.breakdownApi(response));
    },
  },

  beforeMount() {
    this.callApi();
  },
  //listen for prop change then re-search the api
  watch: {
    search: function () {
      this.callApi();
    },
  },
};
</script>
