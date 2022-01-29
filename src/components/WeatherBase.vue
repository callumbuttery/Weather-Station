<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-card color="blue">
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
          </v-col>
        </v-card>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6" md="4" >
        <CurrentWeather/>
      </v-col>
      <v-col cols="12" sm="4" md="8" >
        <NextThreeDays/>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import CurrentWeather from "./CurrentWeather";
import NextThreeDays from "./NextThreeDays";

export default {
  name: "WeatherBase",
  components: {
    CurrentWeather,
    NextThreeDays,
  },
};
</script>
