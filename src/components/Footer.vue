<template>
<b-container fluid class="bg-info">
<b-row>
  <b-col>
    <footer>hi</footer>
  </b-col>
</b-row>
</b-container>
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
      let hero = this.searchInput;
      let url = `https://superhero-search.p.rapidapi.com/?hero=${hero}`;
      const headers = {
        "x-rapidapi-host": "superhero-search.p.rapidapi.com",
        "x-rapidapi-key": "a334f7c84cmsh347049998c599c2p15bfc1jsnf03181b5e460"
      };

      axios
        .get(url, { headers: headers })
        .then(response => response.data)
        .then(response => {
          let data = response;
          console.log(data);
          this.$emit("search", data);
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
  color:blue;
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
