<template>
  <div class="hello">
    <div class="countries">
      <h3>WeJapa Countries</h3>
      <br />
      <label for="country">Choose a Country:</label>
      <!-- <p>  {{get}} </p> -->
      <select name="country" v-model="selectedCountryIndex">
        <!-- <option value="" ></option> -->
        <option
          v-for="(country, index) in getCountry"
          :key="index"
          :value="index"
          selected="Please select one"
        >
          {{ country.name }}</option
        >
      </select>
      <label class="selected"> Selected: {{ selectedCountry }} </label>
      <br />
      <br />

      <label for="country">Choose a State:</label>
      <select name="state" v-model="selectedStateIndex">
        <option disabled v-if="selectedCountryIndex"
          >Please a {{ selectedCountry }} state</option
        >
        <option
          v-for="(state, index) in selectedCountryStates"
          :key="index"
          :value="index"
          >{{ state.name }}</option
        >
      </select>
      <label class="selected"> Selected: {{ selectedState }}</label>
      <br />
      <br />

      <label for="country">Choose a City:</label>
      <select name="cities" v-model="selectedCity">
        <option disabled v-if="selectedStateIndex"
          >Please choose a {{ selectedState }} cities</option
        >
        <option
          v-for="(city, index) in selectedStateCities"
          :key="index"
          :value="city.name"
          >{{ city.name }}</option
        >
      </select>
      <label class="selected"> Selected: {{ selectedCity }}</label>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  data() {
    return {
      getCountry: [{ name: "Countires loading", states: [{}] }],
      getIndex: "",
      selectedCountryIndex: "",
      selectedStateIndex: "",
      selectedCity: ""
    };
  },
  computed: {
    selectedCountry() {
      let index = parseInt(this.selectedCountryIndex);
      return this.getCountry[index].name;
    },
    selectedCountryStates() {
      let index = parseInt(this.selectedCountryIndex);
      return this.getCountry[index].states;
    },
    selectedState() {
      let index = parseInt(this.selectedStateIndex);
      return this.selectedCountryStates[index].name;
    },
    selectedStateCities() {
      let index = parseInt(this.selectedStateIndex);
      return this.selectedCountryStates[index].cities;
    }
  },
  // props: {
  //     // getCountry:[]
  // },
  created() {
    let url =
      "https://raw.githubusercontent.com/dr5hn/countries-states-cities-database/master/countries%2Bstates%2Bcities.json";

    axios.get(url).then(res => {
      this.getCountry = res.data;
    });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.hello {
  margin-left: 0;
  margin-right: 0;
  // width: 50%;
  padding: 5%;
}
.countries {
  padding: 10% 5%;
  background: rgb(60, 121, 190);
  text-align: left;
}
.selected {
  font-size: 1.2em;
  margin-left: 8%;
  text-align: right;
}
label {
  font-size: 1.4em;
}
select {
  border: 0;
  height: 30px;
}
h3 {
  margin: 40px 0 0;
  margin-bottom: 5%;
  font-size: 2em;
  text-align: center;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
