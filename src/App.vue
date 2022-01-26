<template>
  <v-app>
    <v-main>
      <WeatherBase />
    </v-main>
  </v-app>
</template>

<script>
import WeatherBase from "./components/WeatherBase";

export default {
  name: "App",

  components: {
    WeatherBase,
  },

  data: () => ({
    //
  }),
};
</script>
