<template>
  <form @submit.prevent="searchPokemonUrl" class="search mt-5">
    <input placeholder="Search" type="text" v-model="searchText" />
  </form>
</template>

<script>
import axios from "axios";

export default {
  props: ["apiUrl"],
  data() {
    return {
      searchText: ""
    };
  },
  methods: {
    searchPokemonUrl(url) {
      if (this.searchText !== "") {
        this.$emit(
          "searchPokemonUrl",
          this.apiUrl + this.searchText.toLowerCase()
        );
      }
      this.searchText = "";
    }
  }
};
</script>

<style lang="scss" scoped>
.search {
  input {
    width: calc(100% - 30px);
    height: 40px;
    padding: 0 15px;
    border: none;
    font-size: 20px;
    text-align: center;
    border-radius: 10px;
    -webkit-box-shadow: 0px 0px 5px 0px rgba($midnight, 0.4);
    -moz-box-shadow: 0px 0px 5px 0px rgba($midnight, 0.4);
    box-shadow: 0px 0px 5px 0px rgba($midnight, 0.4);
    outline: none;
  }
}
</style>
