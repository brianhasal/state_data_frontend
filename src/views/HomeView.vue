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
      this.indexStateAbbr();
      this.indexStateData();
    },
    methods: {
      indexStateAbbr: function () {
        axios.get("/states.json").then((response) => {
          console.log(response.data);
          this.abbr_array = response.data;
        })
      },
      indexStateData: function () {
        axios.get("/data.json").then((response) => {
          console.log("indexing state data", response.data);
          this.state_data_array = response.data;
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

    <div v-for="byState in state_data_array" v-bind:key="byState.state">
      <h2>{{byState["state"]}}</h2>
      <h2>{{byState["median_household_income"]}}</h2>
      <h2>{{byState["state"]}}</h2>
    </div>

  </div>
</template>

<style></style>