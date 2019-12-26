<template>
  <div>
    <b-container fluid id="app">
      <NavBar @search="search" msg="Welcome to Your Vue.js App" />
    </b-container>
    <b-container>
      <div v-if="hero">
        <b-row>
          <b-col>
            <h1 class="text-center">{{hero.name}}</h1>
            <img :src="hero.images.lg" />
          </b-col>
          <b-col>
            <b-card class="bg-dark" style="margin-top:50%">
              <ul class="list-unstyled">
                <li>Alignment: {{hero.biography.alignment}}</li>
                <li>Alter Egos: {{hero.biography.alterEgos}}</li>
                <li>First Appearance: {{hero.biography.firstAppearance}}</li>
                <li>Full Name: {{hero.biography.fullName}}</li>
              </ul>
              <p>Connections: {{hero.connections.groupAffiliation}} </p>
              <p>Family: {{hero.connections.relatives}} </p>
            </b-card>
          </b-col>
        </b-row>
      </div>
    </b-container>
  </div>
</template>

<script>
import NavBar from "./components/NavBar.vue";

export default {
  name: "app",
  components: {
    NavBar
  },
  data() {
    return {
      hero: null
    };
  },
  methods: {
    search(data) {
      console.log(data);
      console.log("success");
      this.hero = data;
    }
  }
};
</script>

<style>
html,
body {
  font-family: "Roboto", Helvetica, Arial, sans-serif;
}
body {
  color: white;
  background-color: black;
}

i {
  color: black;
}
</style>
