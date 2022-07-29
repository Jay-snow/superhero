<template>
  <form @submit.prevent="submitSearch">
    <b-row class="navbar shadow">
      <b-col col>
        <nav class="d-flex justify-content-between align-items-center">
          <h1>
            Super
            <span id style="color:yellow;" class="text-black">Hero</span> Search
          </h1>

          <div style="width:800px;" class="inner-addon right-addon">
            <div @click="submitSearch">
              <i class="material-icons">search</i>
            </div>
            <b-input
              list="hero-list"
              id="search"
              placeholder="Search for superhero..."
              v-model="searchInput"
              style="font-size:1.5em;"
            ></b-input>
            <datalist id="hero-list">
              <option :key="size" v-for="size in sizes">{{ size }}</option>
            </datalist>
          </div>

          <b-btn variant="success" @click="randomHero" style="font-size:1.3em;">
            Random Hero
            <b-spinner v-if="dataFetching" small label="Spinning"></b-spinner>
          </b-btn>
          <div></div>
          <div></div>
        </nav>
      </b-col>
    </b-row>
  </form>
</template>

<script>
import axios from "axios";

export default {
  name: "NavBar",
  data() {
    return {
      dataFetching: false,
      searchInput: "",
      sizes: [
        "Dick Grayson",
        "Hulk",
        "Thor",
        "Thing",
        "Beast",
        "Captian America",
        "Big Barda",
        "Black Canary",
        "Spidergwen",
        "Jessica Jones",
        "Catwoman",
        "Supergirl",
        "Captain Marvel",
        "Hawkeye",
        "Black Widow",
        "Spawn",
        "Hellboy",
        "abe sapien",
        "Amazo",
        "Magneto",
        "Storm",
        "Iron Man",
        "Superman",
        "Batman",
        "X-23",
        "Wolverine",
        "Cyclops",
        "poision ivy",
        "Harley quinn",
        "flash",
        ""
      ]
    };
  },
  methods: {
    submitSearch() {
      console.log("Search submittedd");
    
      let hero = this.searchInput;

      if (hero.toLowerCase() == "batman") {
        hero = "Bruce wayne";
      }

      if (hero.toLowerCase() == "batman beyond") {
        hero = "batman";
      }

      if (
        hero.toLowerCase() == "wonder woman" ||
        hero.toLowerCase() == "wonderwoman"
      ) {
        hero = "diana prince";
      }

       const options = {
        method: "GET",
        url: "https://superhero-search.p.rapidapi.com/api/",
        params: { hero: hero },
        headers: {
         'X-RapidAPI-Key': 'a334f7c84cmsh347049998c599c2p15bfc1jsnf03181b5e460',
         'X-RapidAPI-Host': 'superhero-search.p.rapidapi.com'
        },
      };
      
      console.log(options);

      axios
        .request(options)
        .then(response => {
          console.log(response.data);
          this.$emit("search", response.data);
        })
        .catch(error => {
          console.error(error);
        });

      // let url = `https://superhero-search.p.rapidapi.com/?hero=${hero}`;
      // const headers = {
      //   "x-rapidapi-host": "superhero-search.p.rapidapi.com",
      //   "x-rapidapi-key": "a334f7c84cmsh347049998c599c2p15bfc1jsnf03181b5e460"
      // };

      // axios
      //   .get(url, { headers: headers })
      //   .then(response => response.data)
      //   .then(response => {
      //     let data = response;
      //     console.log(data);
      //     this.$emit("search", data);
      //   });
    },
    randomHero() {
      let randomid = Math.floor(Math.random() * 600);
      this.dataFetching = true;

      const options = {
        method: "GET",
        url: "https://superhero-search.p.rapidapi.com/api/",
        params: { hero: this.sizes[Math.floor(Math.random() * this.sizes.length)] },
        headers: {
          "x-rapidapi-host": "superhero-search.p.rapidapi.com",
          "x-rapidapi-key":
            "1b8487d47emsh565f8396bd255abp10292bjsn48d02715b657",
        },
      };

     axios
        .request(options)
        .then(response => {
          console.log(response.data);
          this.$emit("search", response.data);
        })
        .catch(error => {
          console.error(error);
        });

        
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.navbar {
  background-color: darkred;
}

.inner-addon {
  position: relative;
}

/* style icon */
.inner-addon .material-icons {
  position: absolute;
  padding: 10px;
}

.material-icons {
  cursor: pointer;
}

.material-icons:hover {
  color: blue;
}

/* align icon */
.left-addon .material-icons {
  left: 0px;
}
.right-addon .material-icons {
  right: 0px;
}

/* add padding  */
.left-addon input {
  padding-left: 30px;
}
.right-addon input {
  padding-right: 30px;
}
</style>
