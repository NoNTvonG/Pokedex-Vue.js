<template>
  <div class="pokemon-types">
    <span v-for="type in types" :class="[type, 'type']">{{ type }}</span>
  </div>
</template>

<script>
export default {
  props: ["types"]
};
</script>

<style lang='scss' scoped>
.pokemon-types {
  display: flex;

  .type {
    padding: 2px 10px;
    margin: 0 5px;
    border: solid 1px $asphalt;
    border-radius: 25px;
  }
  :first-child {
    margin-left: 0;
  }
}
.poison {
  background-color: $poison;
}
.psychic {
  background-color: $psychic;
}
.normal {
  background-color: $normal;
}
.grass {
  background-color: $grass;
}
.ground {
  background-color: $ground;
}
.ice {
  background-color: $ice;
}
.fire {
  background-color: $fire;
}
.rock {
  background-color: $rock;
}
.dragon {
  background-color: $dragon;
}
.water {
  background-color: $water;
}
.bug {
  background-color: $bug;
}
.dark {
  background-color: $dark;
}
.fighting {
  background-color: $fighting;
}
.ghost {
  background-color: $ghost;
}
.steel {
  background-color: $steel;
}
.flying {
  background-color: $flying;
}
.electric {
  background-color: $electric;
}
.fairy {
  background-color: $fairy;
}
</style>