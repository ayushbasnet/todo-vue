<template>
  <div id="app">
    <ToDo />
  </div>
</template>

<script>
import ToDo from "./components/ToDo.vue";

export default {
  name: "App",
  components: {
    ToDo,
  },
};
</script>

<style>
#app {
  width: 50%;
}

body {
  background-color: #eeeeee;
  font-family: "Montserrat", sans-serif;
  display: grid;
  grid-template-rows: auto;
  justify-items: center;
  padding-top: 50px;
}

body,
html {
  margin: 0;
  height: 100%;
}
</style>
