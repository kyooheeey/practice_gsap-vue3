<template>
  <div id="nav">
    <Header />
    <Banner />
    <Panels />
  </div>
</template>

<script>
import Header from "./components/Header.vue"
import Banner from "./components/Banner.vue"
import Panels from "./components/Panels.vue"

export default {
    name: "App",
    components: {
        Header,
        Banner,
        Panels
    }
}
</script>

<style>
body {
  background-color: #F5F5F5;
  font-family: 'Poppins', sans-serif;
  margin: 0px;
}

a {
  text-decoration: none;
}
</style>