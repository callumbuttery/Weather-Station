<template>
  <v-container>
    <v-row class="justify-center" no-gutters>
      <v-card>
        <v-text-field
          :rules="rules"
          hide-details="auto"
          class="centered-input"
          outline
          single-line
          placeholder="Search Location"
        ></v-text-field
      ></v-card>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "Search",
};
</script>

<style>
.centered-input input {
  text-align: center;
}
</style>
