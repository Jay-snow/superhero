<template>
    <b-row class="body">
      <b-col>
        <div >
          <h1>
            The best heroes
          </h1>
        </div>
      </b-col>
    </b-row>
</template>

<script>
export default {
  name: "Arena",
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .body {
    background-color:darkgrey;
  }
</style>
