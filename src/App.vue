<template>
  <div class="results d-flex flex-column">
    <b-container fluid style="flex:1 0 auto;">
      <NavBar @search="search" />
      <transition name="fade">
        <div class="hero_results" v-if="hero">
          <b-row>
            <b-col class="text-center">
              <h1>{{hero.name}}</h1>
              <img class="img-fluid shadow-lg rounded" :src="hero.images.lg" />
            </b-col>
            <b-col>
              <b-card class="shadow-lg " style="margin-top:4rem;font-size:1.5em;background-color:rgba(0,0,0,0.3);">
                <small>Real Name</small>
                <h3>{{hero.biography.fullName}}</h3>

                <small>First Apperance</small>
                <h3>{{hero.biography.firstAppearance}}</h3>


          
                <!-- <p>Family: {{hero.connections.relatives}}</p> -->

                <h5>Combat</h5>
                <b-progress
                  height="2rem"
                  animated
                  variant="danger"
                  :value="hero.powerstats.combat"
                  :max="100"
                  show-progress
                  class="mb-3"
                ></b-progress>

                <h5>Durability</h5>
                <b-progress
                  height="2rem"
                  animated
                  variant="success"
                  :value="hero.powerstats.durability"
                   :max="100"
                  show-value
                  class="mb-3"
                ></b-progress>

                <h5>Intelligence</h5>
                <b-progress
                  height="2rem"
                  animated
                  :value="hero.powerstats.intelligence"
                   :max="100"
                  show-progress
                  class="mb-3"
                ></b-progress>

                <h5>Speed</h5>
                <b-progress
                  height="2rem"
                  animated
                  variant="info"
                  :value="hero.powerstats.speed"
                  :max="100"
                  :precision="2"
                  show-value
                  class="mb-3"
                ></b-progress>

                <h5>Strength</h5>
                <b-progress
                  animated
                  variant="dark"
                  height="2rem"
                  :value="hero.powerstats.strength"
                  :max="100"
                  :precision="2"
                  show-progress
                  class="mb-3"
                ></b-progress>
              </b-card>
            </b-col>
          </b-row>
        </div>
      </transition>
    </b-container>
    <Footer class="d-none flex-shrink-0"></Footer>
  </div>
</template>

<script>


import NavBar from "./components/NavBar.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "app",
  components: {
    NavBar,
    Footer
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
  },
};

// dots is an array of Dot objects,
// mouse is an object used to track the X and Y position
   // of the mouse, set with a mousemove event listener below
var dots = [],
    mouse = {
      x: 0,
      y: 0
    };

// The Dot object used to scaffold the dots
var Dot = function() {
  this.x = 0;
  this.y = 0;
  this.node = (function(){
    var n = document.createElement("div");
    n.className = "trail";
    document.body.appendChild(n);
    return n;
  }());
};
// The Dot.prototype.draw() method sets the position of 
  // the object's <div> node
Dot.prototype.draw = function() {
  this.node.style.left = this.x + "px";
  this.node.style.top = this.y + "px";
};

// Creates the Dot objects, populates the dots array
for (var i = 0; i < 12; i++) {
  var d = new Dot();
  dots.push(d);
}

// This is the screen redraw function
function draw() {
  // Make sure the mouse position is set everytime
    // draw() is called.
  var x = mouse.x,
      y = mouse.y;
  
  // This loop is where all the 90s magic happens
  dots.forEach(function(dot, index, dots) {
    var nextDot = dots[index + 1] || dots[0];
    
    dot.x = x;
    dot.y = y;
    dot.draw();
    x += (nextDot.x - dot.x) * .6;
    y += (nextDot.y - dot.y) * .6;

  });
}

addEventListener("mousemove", function(event) {
  //event.preventDefault();
  mouse.x = event.pageX;
  mouse.y = event.pageY;
});

// animate() calls draw() then recursively calls itself
  // everytime the screen repaints via requestAnimationFrame().
function animate() {
  draw();
  requestAnimationFrame(animate);
}

// And get it started by calling animate().
animate();


</script>

<style>
html,
body {
  font-family: "Bangers", Helvetica, Arial, sans-serif;
  width: 100%;
  height: 100%;
}

body {
  color: white;
  background-image: url("assets/background.jpg");
  background-size: cover;
  min-height: 100%;
  display: flex;
  flex-direction: column;
}

.results {
  min-height: 100%;
}

footer {
  flex-shrink: 0;
}

.autocomplete-items {
  position: absolute;
  border: 1px solid #d4d4d4;
  border-bottom: none;
  border-top: none;
  z-index: 99;
  /*position the autocomplete items to be the same width as the container:*/
  top: 100%;
  left: 0;
  right: 0;
}

.autocomplete-items div {
  padding: 10px;
  cursor: pointer;
  background-color: #fff;
  border-bottom: 1px solid #d4d4d4;
}

/*when hovering an item:*/
.autocomplete-items div:hover {
  background-color: #e9e9e9;
}

/*when navigating through the items using the arrow keys:*/
.autocomplete-active {
  background-color: DodgerBlue !important;
  color: #ffffff;
}

i {
  color: black;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

.trail { /* className for the trail elements */
    position: absolute;
    height: 6px; width: 6px;
    border-radius: 3px;
    background: red;
    pointer-events: none;
  }
</style>
