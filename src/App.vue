<template>
  <div id="app">
    <NavBar />
    <router-view />
    <Pokedex />
    <Footer />
  </div>
</template>

<script>
import NavBar from "./components/NavBar";
import Pokedex from "./views/Pokedex";
import Footer from "./components/Footer";

export default {
  name: "app",
  components: {
    NavBar,
    Pokedex,
    Footer,
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@300;400;500;600;700&family=Russo+One&display=swap");
// Стилізація всіх скролбарів
::-webkit-scrollbar {
  width: 8px;
  background-color: #f5f5f5;
}
// Стильізація повзунка в скролбарі
::-webkit-scrollbar-thumb {
  width: 8px;
  background-color: $alizarin;
}

#app {
  font-family: "Roboto Mono", Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  // Забирае підсвічення блоків синім коліром. Замітно на телефонах
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100vh;
}
a {
  text-decoration: none;
}
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
