<template>
  <div id="app">
    <imageBrowser />
  </div>
</template>


<script lang="ts">
import Vue from "vue";
import imageBrowser from "@/components/imageBrowser.vue";
import Component from "vue-class-component";
@Component({
  components: {
    imageBrowser
  }
})
export default class App extends Vue {}
</script>
<style lang="scss">
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  padding: 0;
}
#app {
  font-family: Calibri, Candara, Segoe, Segoe UI, Optima, Arial, sans-serif;
}
header {
  background: #333;
  height: 60px;
}
.header-text {
  text-align: center;
  font-size: 42px;
  color: white;
  font-weight: 600;
}
.Search-att {
  padding: 1.5rem;
  border-bottom: 1px solid #e7e7e7;
  display: flex;
  justify-content: center;
}
.Search-att input[type="text"] {
  width: 15%;
  height: 25px;
  text-indent: 15px;
}
.Search-att input[type="submit"] {
  height: 25px;
  background: #333;
  color: white;
}
.image-box {
  border-radius: 5px 5px 0 0;
  width: 200px;
  height: 200px;
  object-fit: cover;
  padding: 5px;
}
.Container-images {
  padding-right: 75px;
  padding-left: 75px;
  height: 600px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  overflow-y: scroll;
}
@media only screen and(max-width: 1024px) {
  .Search-att input[type="text"] {
    width: auto;
  }
}
</style>
