<script>
  import axios from "axios";
  export default {
    data: function () {
      return {
        state_data_array: [],
        abbr_array: []
      };
    },
    created: function () {
      this.indexStateData();
    },
    methods: {
      indexStateData: function () {
        axios.get("/states.json").then((response) => {
          console.log(response.data);
          this.abbr_array = response.data;
        })
      }
    },
  };
</script>

<template>
  <div class="home">
    <h1>States by Abbreviation</h1>
    <p>{{this.abbr_array}}</p>

    <div v-for="state in abbr_array" v-bind:key="state.name">
      <h2>{{state["state"]}}</h2>
      <h3>{{state["abbrev"]}}</h3>
      <h3>{{state["code"]}}</h3>
    </div>
  </div>
</template>

<style></style>