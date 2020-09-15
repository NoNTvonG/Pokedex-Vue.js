<template>
  <div class="mt-5 mb-5">
    <transition-group appear name="slide" class="pokemon-arr" tag="div">
      <!-- Pokemon cards -->
      <article
        class="card"
        v-for="(pokemon, index) in pokemons"
        :key="pokemon.name"
        @click="setPokemonUrl(pokemon.url)"
      >
        <!-- :style="'transition-delay:' + 1 * index + 's'" -->
        <!-- Pokemon picture -->
        <img
          :src="imageUrl + pokemon.id + '.png'"
          alt="pokemon"
          class="card-img pt-2 pb-2"
        />
        <!-- Pokemon Name -->
        <div class="card-body">
          <p class="card-title">{{ pokemon.name }}</p>
        </div>
      </article>
    </transition-group>
    <!-- анімація спінера на який причіплений трігер для підгрузки данних -->
    <div class="scroll-trigger mt-5 mb-5" ref="infinitescrolltrigger">
      <div class="lds-dual-ring"></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: ["apiUrl", "imageUrl"],
  data() {
    return {
      pokemons: [],
      nextUrl: "",
      currentUrl: "",
    };
  },
  created() {
    this.currentUrl = this.apiUrl;
    this.fetchData();
  },
  methods: {
    fetchData() {
      axios
        .get(this.currentUrl)
        .then(({ data }) => {
          this.nextUrl = data.next;
          data.results.forEach((pokemon) => {
            pokemon.id = pokemon.url
              .split("/")
              .filter(function(part) {
                return !!part;
              })
              .pop();
            this.pokemons.push(pokemon);
          });
        })
        .catch(({ err }) => {
          console.log(err);
        });
    },
    // трігер для загрузки даних
    scrollTrigger() {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach((entry) => {
          if (entry.intersectionRatio > 0 && this.nextUrl) {
            this.next();
          }
        });
      });

      observer.observe(this.$refs.infinitescrolltrigger);
    },
    // показати наступних покемонів
    next() {
      this.currentUrl = this.nextUrl;
      this.fetchData();
    },
    setPokemonUrl(url) {
      this.$emit("setPokemonUrl", url);
    },
  },
  mounted() {
    this.scrollTrigger();
  },
};
</script>

<style lang="scss" scoped>
.slide-enter {
  opacity: 0;
  transform: scale(0.5);
}
.slide-enter-active {
  transition: all 0.5s ease;
  transition-delay: 0.5s;
}
.pokemon-arr {
  display: grid;
  grid-template-columns: repeat(auto-fit, 200px);
  grid-gap: 42px;
  justify-content: center;

  .card {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border: 1px solid $clouds;
    border-radius: 10px;
    box-shadow: 0px 0px 5px 2px rgba($concrete, 0.3);
    cursor: pointer;
    transition: 0.3s;

    &:hover {
      transform: translateY(-10px);
      box-shadow: 0px 10px 5px 2px rgba($concrete, 0.5);
    }

    .card-img {
      height: 96px;
      width: 96px;
    }

    .card-body {
      width: 100%;
      .card-title {
        font-size: 20px;
        font-weight: 700;
        text-align: center;
        text-transform: capitalize;
        background-color: $clouds;
        margin: 0;
        padding: 1rem 0;
        border-bottom-left-radius: 9px;
        border-bottom-right-radius: 9px;
      }
    }
  }
}
.scroll-trigger {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
