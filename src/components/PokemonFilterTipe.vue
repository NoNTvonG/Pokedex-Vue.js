<template>
  <div class="pokemon-filter-type mt-3">
    <form class="types-wrapper pt-2 pb-2" v-on:change="filterPokemonUrl">
      <h3 class="type-header pb-2">Select pokemon type</h3>
      <transition name="slide-toggle">
        <transition-group
          appear
          name="slide"
          class="pokemon-arr pb-2"
          tag="ul"
          v-if="typesShow"
        >
          <li
            v-for="(type, index) in pokemonTypes"
            :key="type.name"
            :style="'transition-delay:' + 0.1 * index + 's'"
          >
            <input
              type="checkbox"
              :name="type.name"
              :value="type.url"
              :id="type.name"
              v-model="selectedType"
              @change="unChecked"
            />
            <label :for="type.name">
              <img
                class="type-picture"
                :class="type.name"
                :src="require('../assets/types/' + type.name + '.svg')"
              />
              {{ type.name }}
            </label>
          </li>
        </transition-group>
      </transition>
      <img
        @click="showTypesPanel"
        src="@/assets/arrow.svg"
        class="arrow"
        :class="{ 'arrow-rewers': typesShow }"
        alt="arrow"
      />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: ["apiUrl", "typeUrl"],
  data() {
    return {
      pokemonTypes: [],
      selectedType: [],
      typesShow: false,
    };
  },
  computed: {
    name() {},
  },
  methods: {
    showTypesPanel() {
      this.typesShow = !this.typesShow;
    },
    filterPokemonUrl(url) {
      this.$emit("filterPokemonUrl", this.selectedType);
    },
    unChecked(e) {
      this.selectedType = [];
      if (e.target.checked) {
        this.selectedType.push(e.target.value);
      } else {
        this.selectedType.push(this.apiUrl);
      }
    },
  },
  mounted: function() {
    // При першій загрузці сторінки викликаємо функцію
    // для того щоб вибраний тип передавня вище інакше
    // сторінка буде пуста доки сам не жмякнеш на All
    this.filterPokemonUrl();
  },
  beforeMount: function() {
    this.$nextTick(function() {
      axios
        .get(this.typeUrl)
        .then(({ data }) => {
          this.pokemonTypes.push({ name: "all", url: this.apiUrl });
          data.results.forEach((value) => {
            if ((value.name != "shadow") & (value.name !== "unknown")) {
              this.pokemonTypes.push(value);
            }
          });
        })
        .catch(({ err }) => {
          console.log(err);
        });
    });
    // При першій загрузці передаємо апі в список тим самим чекбокс All включається
    this.selectedType = [this.apiUrl];
  },
};
</script>

<style lang="scss" scoped>
.pokemon-filter-type {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  .slide-enter {
    opacity: 0;
    transform: scale(0.5);
  }
  .slide-enter-active {
    transition: all 0.5s ease;
  }

  .types-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    border: 1px solid $clouds;
    border-radius: 10px;
    box-shadow: 0px 0px 5px 0px rgba($midnight, 0.4);

    .slide-toggle-enter-active {
      height: 100%;
    }
    .slide-toggle-enter,
    .slide-toggle-leave,
    .slide-toggle-leave-active {
      height: 0;
    }

    .type-header {
      color: $concrete;
      font-weight: 500;
      text-align: center;
      margin: 0;
    }
    .arrow {
      width: 20px;
      transition: 0.5s;
      margin: 0 auto;
    }
    .arrow-rewers {
      transform: rotateX(180deg) !important;
    }
    ul {
      display: grid;
      grid-template-columns: repeat(auto-fit, 150px);
      grid-gap: 10px;
      justify-content: center;

      li {
        border: 1px solid $clouds;
        border-radius: 10px;
        box-shadow: 0px 0px 5px 0px rgba($silver, 0.4);
        // border-bottom: 2px solid $asphalt;

        input[type="checkbox"] {
          display: none;
          cursor: pointer;
        }
        input[type="checkbox"]:checked ~ label {
          background-color: $clouds;
          border-radius: 10px;
          font-weight: 700;
        }
        label {
          padding: 10px;
          width: calc(100% - 20px);
          height: 100%;
          display: flex;
          align-items: center;
          text-transform: capitalize;
          transition: 0.3s all;
          cursor: pointer;

          .type-picture {
            margin-right: 10px;
            height: 20px;
            padding: 5px;
            border-radius: 100%;
            &:hover {
              filter: saturate(200%);
              cursor: pointer;
            }
          }
        }
        .bug {
          background: $bug;
          // box-shadow: 0 0 20px $bug;
        }

        .dark {
          background: $dragon;
          // box-shadow: 0 0 20px $dragon;
        }

        .dragon {
          background: $dragon;
          // box-shadow: 0 0 20px $dragon;
        }

        .electric {
          background: $electric;
          // box-shadow: 0 0 20px $electric;
        }

        .fire {
          background: $fire;
          // box-shadow: 0 0 20px $fire;
        }

        .fairy {
          background: $fighting;
          // box-shadow: 0 0 20px $fighting;
        }

        .fighting {
          background: $fighting;
          // box-shadow: 0 0 20px $fighting;
        }

        .flying {
          background: $flying;
          // box-shadow: 0 0 20px $flying;
        }

        .ghost {
          background: $ghost;
          // box-shadow: 0 0 20px $ghost;
        }

        .grass {
          background: $grass;
          // box-shadow: 0 0 20px $grass;
        }

        .ground {
          background: $ground;
          // box-shadow: 0 0 20px $ground;
        }

        .ice {
          background: $ice;
          // box-shadow: 0 0 20px $ice;
        }

        .normal {
          background: $normal;
          // box-shadow: 0 0 20px $normal;
        }

        .poison {
          background: $poison;
          // box-shadow: 0 0 20px $poison;
        }

        .psychic {
          background: $psychic;
          // box-shadow: 0 0 20px $psychic;
        }

        .rock {
          background: $rock;
          // box-shadow: 0 0 20px $rock;
        }

        .steel {
          background: $steel;
          // box-shadow: 0 0 20px $steel;
        }

        .water {
          background: $water;
          // box-shadow: 0 0 20px $water;
        }
      }
    }
  }
}
</style>
