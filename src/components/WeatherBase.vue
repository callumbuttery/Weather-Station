<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-card color="purple lighten-1" elevation="14">
          <v-img
            :src="require('../assets/weather.png')"
            class="my-3"
            contain
            height="200"
          />
          <v-col class="mb-4">
            <v-card-title class="display-2 mb-2 justify-center"
              >Weather Station</v-card-title
            >
            <v-row>
              <Search v-on:changeLocation="updateLocation($event)"/>
            </v-row>
          </v-col>
        </v-card>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6" md="4">
        <CurrentWeather :search="this.$props.search"/>
      </v-col>
      <v-col cols="12" sm="4" md="8">
        <NextThreeDays :search="this.$props.search"/>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import CurrentWeather from "./CurrentWeather";
import NextThreeDays from "./NextThreeDays";
import Search from "./Search";

export default {
  name: "WeatherBase",
  props: {
    search: String,
  },
  components: {
    CurrentWeather,
    NextThreeDays,
    Search,
  },
  methods: {
    updateLocation: function(location) {
      if (location) {
        this.$props.search = location;
      }
    } 
  },
};
</script>
