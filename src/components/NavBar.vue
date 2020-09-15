<template>
  <div class="navbar">
    <img src="@/assets/logo.webp" alt="logo" />
    <router-link to="/" class="nav-link">Pokedex</router-link>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
$nav_height: 70px;

.navbar {
  height: $nav_height;
  padding: 0 1em;
  background-color: $alizarin;
  display: flex;
  align-items: center;

  img {
    height: 50px;
    padding-right: 10px;
  }

  a {
    color: $clouds;
    font-family: "Russo One", sans-serif;
    font-size: 40px;
    line-height: $nav_height;
  }
}
</style>
