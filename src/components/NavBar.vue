<template>
  <b-row class="navbar">
    <b-col col md="4">
      <b-btn @click="submitSearch">Search</b-btn>
    </b-col>
    <b-col col>
      <b-input v-model="searchInput"></b-input>
    </b-col>
  </b-row>
</template>

<script>
import axios from "axios";

export default {
  name: "NavBar",
  props: {
    msg: String
  },
  data() {
    return {
      searchInput: ""
    };
  },
  methods: {
    submitSearch() {
      console.log(this.searchInput);
      let hero = this.searchInput;
      let url = `https://superhero-search.p.rapidapi.com/?hero=${hero}`;
      const headers = {
        "x-rapidapi-host": "superhero-search.p.rapidapi.com",
        "x-rapidapi-key": "a334f7c84cmsh347049998c599c2p15bfc1jsnf03181b5e460"
      };

      axios.get(url,{headers: headers}).then(function (response){
        console.log(response);
      })
      

    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.navbar {
  background-color: darkred;
}
</style>
