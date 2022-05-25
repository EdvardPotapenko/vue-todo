<template>
  <div id="app">
    <vue-header />
    <router-view />
  </div>
</template>

<script>
import VueHeader from "./components/layouts/VueHeader.vue";
export default {
  name: "app",
  components: {
    VueHeader,
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
