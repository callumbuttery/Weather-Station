<template>
  <v-container>
    <v-row no-gutters>
      <v-col>
        <v-card>
          <v-card-title class="text-h4 justify-center"
            >5 Day Forecast</v-card-title>
            <v-card-subtitle></v-card-subtitle>
          </v-card
        ></v-col
      ></v-row
    ></v-container
  >
</template>

<script>
import axios from "axios";

export default {
  name: "NextFiveDays",

  data() {
    return {
      fiveDays: "",
    };
  },

  async beforeMount() {
    await axios
      .get(
        `http://api.weatherapi.com/v1/forecast.json?key=${process.env.VUE_APP_WEATHER_API_KEY}&q=London&days=5&aqi=no&alerts=no`
      )
      .then((response) => (this.fiveDays = response.data.forecast));

    //console.log(this.fiveDays);
  },
};
</script>
