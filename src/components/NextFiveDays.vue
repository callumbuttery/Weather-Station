<template>
  <v-container>
    <v-row no-gutters>
      <v-col>
        <v-card>
          <v-card-title class="text-h4 justify-center"
            >3 Day Forecast</v-card-title
          >

          <v-row no-gutters>
            <v-col>
              <v-card class="pa-2 text-center" outlined tile>
                <v-img
                  class="mx-auto"
                  :src="this.dayOne.condition.icon"
                  max-height="50"
                  max-width="50"
                ></v-img>
                <v-card-subtitle class="text-h5 justify-center">{{
                  this.dateToDateOne
                }}</v-card-subtitle>
              </v-card>
            </v-col>
            <v-col>
              <v-card class="pa-2 text-center" outlined tile>
                <v-img
                  class="mx-auto"
                  :src="this.dayTwo.condition.icon"
                  max-height="50"
                  max-width="50"
                ></v-img>
                <v-card-subtitle class="text-h5 justify-center">{{
                  this.dateToDateTwo
                }}</v-card-subtitle>
              </v-card>
            </v-col>
            <v-col>
              <v-card class="pa-2 text-center" outlined tile>
                <v-img
                  class="mx-auto"
                  :src="this.dayThree.condition.icon"
                  max-height="50"
                  max-width="50"
                ></v-img>
                <v-card-subtitle class="text-h5 justify-center">{{
                  this.dateToDateThree
                }}</v-card-subtitle>
              </v-card>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "NextFiveDays",

  data() {
    return {
      fiveDays: "",
      dayOne: "",
      dayTwo: "",
      dayThree: "",
      dateToDateOne: "",
      dateToDateTwo: "",
      dateToDateThree: "",

    };
  },

  methods: {
    breakdown3DayApi: function (apiData) {
      console.log(apiData);
      this.rawApiData = apiData.data.current;
      this.currentLocation = apiData.data.location.name;
      this.currentWeatherImg = apiData.data.current.condition.icon;

      this.dayOne = apiData.data.forecast.forecastday[0].day;
      this.dayTwo = apiData.data.forecast.forecastday[1].day;
      this.dayThree = apiData.data.forecast.forecastday[2].day;

      this.dateToDateOne = apiData.data.forecast.forecastday[0].date;
      this.dateToDateTwo = apiData.data.forecast.forecastday[1].date;
      this.dateToDateThree = apiData.data.forecast.forecastday[2].date;

      //console.log(this.dayThree);
    },
  },

  async beforeMount() {
    await axios
      .get(
        `http://api.weatherapi.com/v1/forecast.json?key=${process.env.VUE_APP_WEATHER_API_KEY}&q=Glasgow&days=5&aqi=no&alerts=no`
      )
      .then((response) => this.breakdown3DayApi(response));
  },
};
</script>
