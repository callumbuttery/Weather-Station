<template>
  <v-container>
    <v-row no-gutters>
      <v-col>
        <v-skeleton-loader class="mx-auto" max-width="300" type="card">
          <v-card class="purple darken-1" elevation="14">
            <v-card-title class="text-h4 white--text justify-center"
              >3 Day Forecast</v-card-title
            >

            <v-card-title
              class="justify-center text-h5 white--text purple darken-1"
            >
              {{ this.currentLocation }}
            </v-card-title>

            <v-row no-gutters>
              <v-col>
                <v-card class="pa-2 text-center purple darken-3" outlined tile>
                  <v-img
                    class="mx-auto"
                    :src="this.days[0].condition.icon"
                    max-height="50"
                    max-width="50"
                  ></v-img>
                  <v-card-subtitle class="text-h5 justify-center white--text">{{
                    this.dates[0]
                  }}</v-card-subtitle>
                  <v-card-subtitle class="text-h6 justify-center white--text">{{
                    this.days[0].avgtemp_c + "C/" + this.days[0].avgtemp_f + "F"
                  }}</v-card-subtitle>
                </v-card>
              </v-col>
              <v-col>
                <v-card class="pa-2 text-center purple darken-4" outlined tile>
                  <v-img
                    class="mx-auto"
                    :src="this.days[1].condition.icon"
                    max-height="50"
                    max-width="50"
                  ></v-img>
                  <v-card-subtitle class="text-h5 justify-center white--text">{{
                    this.dates[1]
                  }}</v-card-subtitle>
                  <v-card-subtitle class="text-h6 justify-center white--text">{{
                    this.days[1].avgtemp_c + "C/" + this.days[1].avgtemp_f + "F"
                  }}</v-card-subtitle>
                </v-card>
              </v-col>
              <v-col>
                <v-card
                  class="pa-2 text-center purple darken-3 white--text"
                  outlined
                  tile
                >
                  <v-img
                    class="mx-auto"
                    :src="this.days[2].condition.icon"
                    max-height="50"
                    max-width="50"
                  ></v-img>
                  <v-card-subtitle class="text-h5 justify-center white--text">{{
                    this.dates[2]
                  }}</v-card-subtitle>
                  <v-card-subtitle class="text-h6 justify-center white--text">{{
                    this.days[2].avgtemp_c + "C/" + this.days[2].avgtemp_f + "F"
                  }}</v-card-subtitle>
                </v-card>
              </v-col>
            </v-row>
          </v-card>
        </v-skeleton-loader>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "NextFiveDays",
  props: {
    search: String,
  },
  data() {
    return {
      fiveDays: "",
      dayOne: "",
      dayTwo: "",
      dayThree: "",
      dateToDateOne: "",
      dateToDateTwo: "",
      dateToDateThree: "",

      days: [],
      dates: [],
      weekdays: [],
      weekday: [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ],
      locationToSearch: "Glasgow",
    };
  },

  methods: {
    breakdown3DayApi: function (apiData) {
      this.rawApiData = apiData.data.current;
      this.currentLocation = apiData.data.location.name;
      this.currentWeatherImg = apiData.data.current.condition.icon;

      const forecast = apiData.data.forecast.forecastday;

      for (var i = 0; i < forecast.length; i++) {
        this.days.push(forecast[i].day);
        this.dates.push(forecast[i].date);
      }
    },
    callApi: async function () {
      await axios
        .get(
          `http://api.weatherapi.com/v1/forecast.json?key=${
            process.env.VUE_APP_WEATHER_API_KEY
          }&q=${
            this.$props.search || this.locationToSearch
          }&days=5&aqi=no&alerts=no`
        )
        .then((response) => this.breakdown3DayApi(response));
    },
  },

  beforeMount() {
    this.callApi();
  },
  watch: {
    search: function () {
      this.callApi();
    },
  },
};
</script>
