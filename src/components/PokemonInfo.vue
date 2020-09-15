<template>
  <div class="info">
    <!-- Pokemon search spinner -->
    <transition name="fade">
      <article v-if="pokemonSearch" class="search-spinner">
        <div class="alert-panel">
          <div class="scroll-trigger mt-5 mb-5">
            <div class="lds-dual-ring"></div>
          </div>
        </div>
      </article>
    </transition>
    <!-- Pokemon found and show information -->
    <transition name="fade">
      <article class="panel" v-if="pokemonFound">
        <div class="panel-icon">
          <img :src="pokemonImg + id + '.png'" alt="pokemon" />
        </div>
        <div class="panel-body">
          <div class="panel-title">
            <h2>{{ name }}</h2>
          </div>
          <div class="panel-text">
            <!-- <p class="mb-3">Pokemon id: {{ id }}</p> -->
            <p class="btm-line">
              <span>HP:</span>
              <span>{{ stats.hp }}</span>
            </p>
            <p class="btm-line">
              <span>Attack:</span>
              <span>{{ stats.attack }}</span>
            </p>
            <p class="btm-line">
              <span>Defense:</span>
              <span>{{ stats.defense }}</span>
            </p>
            <p class="btm-line">
              <span>Special attack:</span>
              <span>{{ stats.specialAttack }}</span>
            </p>
            <p class="btm-line">
              <span>Special defense:</span>
              <span>{{ stats.specialDefense }}</span>
            </p>
            <p class="btm-line">
              <span>Speed:</span>
              <span>{{ stats.speed }}</span>
            </p>
            <br />
            <p class="btm-line">
              <span>Base experience:</span>
              <span>{{ baseExperience }}XP</span>
            </p>
            <p class="btm-line">
              <span>Height:</span>
              <span>{{ height }}</span>
            </p>
            <br />
            <PokemonType :types="types" />
          </div>
          <div class="back mt-3" @click="closeInfo">
            <span>Close</span>
          </div>
        </div>
      </article>
    </transition>
    <!-- Pokemon not found -->
    <transition name="fade">
      <article v-if="!pokemonFound && !pokemonSearch">
        <div class="alert-panel">
          <div class="panel-body">
            <div class="panel-title pt-2 pb-2">
              <h2>Pokemon not found</h2>
            </div>
            <div class="back" @click="closeInfo">
              <span>Close</span>
            </div>
          </div>
        </div>
      </article>
    </transition>
  </div>
</template>

<script>
import axios from "axios";
import PokemonType from "./PokemonType"

export default {
  props: ["pokemonUrl", "pokemonImg", {loaded: Boolean}],
  components: {
    PokemonType
  },
  data() {
    return {
      showInfo: false,
      name: "",
      id: "",
      baseExperience: "",
      height: "",
      types: [],
      stats: {
        hp: "",
        attack: "",
        defense: "",
        specialAttack: "",
        specialDefense: "",
        speed: ""
      },
      pokemonFound: false,
      pokemonSearch: true
    };
  },
  methods: {
    fetchData() {
      axios
        .get(this.pokemonUrl)
        .then(({ data }) => {
          this.name = data.name;
          this.id = data.id;
          this.baseExperience = data.base_experience;
          this.height = data.height;
          this.stats.hp = data.stats.[0].base_stat;
          this.stats.attack = data.stats.[1].base_stat;
          this.stats.defense = data.stats.[2].base_stat;
          this.stats.specialAttack = data.stats.[3].base_stat;
          this.stats.specialDefense = data.stats.[4].base_stat;
          this.stats.speed = data.stats.[5].base_stat;
          this.pokemonFound = true
          this.pokemonSearch = false

          data.types.forEach(t => {
            this.types.push(t.type.name);
          });
        })
        .catch(({ err }) => {
          this.pokemonSearch = false
          this.pokemonFound = false
        });
    },
    closeInfo() {
      this.$emit("closeInfo", this.showInfo);
    }
  },
  mounted() {
    this.fetchData();
  }
};
</script>

<style lang="scss" scoped>
$panel-width: 400px;
$image-size: 80px;

.info {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  position: fixed;
  top: 0;
  left: 0;
  padding: 10px;
  width: calc(100% - 20px);
  height: calc(100vh - 20px);
  background-color: rgba($midnight, 0.7);

  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.5s;
  }
  .fade-enter-active {
    transition-delay: 0.5s;
  }
  .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
    opacity: 0;
  }
}
.panel {
  display: flex;
  align-items: center;
  flex-direction: column;
  width: $panel-width;
  border-radius: 10px;
  padding-top: 50px;
  background-color: $white;
  position: relative;
}
.search-spinner {
  position: absolute;
}
.alert-panel {
  display: flex;
  align-items: center;
  flex-direction: column;
  width: $panel-width;
  border-radius: 10px;
  background-color: $white;
  position: relative;
}
.panel-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100px;
  width: 100px;
  border: 1px solid $asphalt;
  border-radius: 100%;
  position: absolute;
  background-color: $white;
  padding: 10px;
  top: calc((-96px / 2) - 20px);
  box-shadow: 0px 5px 10px 0px rgba($midnight, 0.4);
}
.panel-body {
  width: 100%;

  .panel-title {
    text-align: center;
    text-transform: capitalize;
  }
  .panel-text {
    margin: 20px;
    .btm-line {
      display: flex;
      justify-content: space-between;
      border-bottom: solid 1px $asphalt;
    }
    p {
      margin-top: 10px;
    }
  }
}
img {
  height: $image-size;
  width: $image-size;
}
.back {
  width: calc(100% - 40px);
  text-align: center;
  line-height: 40px;
  height: 40px;
  background-color: $alizarin;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
  padding: 0 20px;
  cursor: pointer;

  span {
    color: $clouds;
  }
}
</style>
