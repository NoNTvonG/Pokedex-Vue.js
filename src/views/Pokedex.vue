<template>
  <div class="container pokedex">
    <PokemonSearch
      @searchPokemonUrl="setPokemonUrl"
      :apiUrl="apiUrl"
      v-bind:class="{ blur: showInfo }"
    />
    <PokemonFilterTipe
      @filterPokemonUrl="filterPokemonUrl"
      :apiUrl="apiUrl"
      :typeUrl="pokemonTypeUrl"
      v-bind:class="{ blur: showInfo }"
    />
    <PokemonList
      v-if="apiUrl == filterTypePokemonUrl"
      :apiUrl="apiUrl"
      :imageUrl="imageUrl"
      @setPokemonUrl="setPokemonUrl"
      v-bind:class="{ blur: showInfo }"
    />
    <PokemonFilterList
      v-if="filterTypePokemonUrl != apiUrl"
      :apiUrl="filterTypePokemonUrl"
      :imageUrl="imageUrl"
      @setPokemonUrl="setPokemonUrl"
      v-bind:class="{ blur: showInfo }"
    />
    <PokemonInfo
      v-if="showInfo"
      :pokemonUrl="pokemonUrl"
      :pokemonImg="imageUrl"
      @closeInfo="closeInfo"
    />
  </div>
</template>

<script>
import PokemonSearch from "../components/PokemonSearch";
import PokemonFilterTipe from "../components/PokemonFilterTipe";
import PokemonList from "../components/PokemonList";
import PokemonFilterList from "../components/PokemonFilterTypeLisr";
import PokemonInfo from "../components/PokemonInfo";

export default {
  name: "Pokedex",
  components: {
    PokemonSearch,
    PokemonFilterTipe,
    PokemonList,
    PokemonFilterList,
    PokemonInfo,
  },
  data() {
    return {
      apiUrl: "https://pokeapi.co/api/v2/pokemon/",
      imageUrl: "https://pokeres.bastionbot.org/images/pokemon/",
      pokemonTypeUrl: "https://pokeapi.co/api/v2/type/",
      pokemonUrl: "",
      showInfo: false,
      filterTypePokemonUrl: "",
    };
  },
  methods: {
    // Показати міні інфо про покемона
    setPokemonUrl(url) {
      this.pokemonUrl = url;
      this.showInfo = true;
    },
    // Закрити міні інформацію про покеммона
    closeInfo(value) {
      this.showInfo = value;
    },
    // Передається URL покемонів первного типу
    filterPokemonUrl(url) {
      this.filterTypePokemonUrl = url[0];
    },
  },
};
</script>

<style lang="scss" scoped>
.pokedex {
  flex-grow: 10;
}
.blur {
  filter: blur(5px);
  transition: 0.3s;
}
</style>
