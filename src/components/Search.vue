<template>
  <v-container>
    <v-row class="justify-center" no-gutters>
      <v-card>
        <v-text-field
          hide-details="auto"
          class="centered-input"
          outline
          single-line
          placeholder="Search Location"
          v-model="input"
        ></v-text-field
      ></v-card>
    </v-row>
    <v-btn class="justify-center" color="secondary" elevation="4" v-on:click="handleInput">Search</v-btn>
  </v-container>
</template>

<script>
export default {
  name: "Search",

  data() {
    return {
      input: "",
    }
  },
  methods: {
    handleInput: function() {
      if (!this.input) {
        alert("Please enter a valid location");
        return;
      }

      
    }
  }
};
</script>

<style>
.centered-input input {
  text-align: center;
}
</style>
