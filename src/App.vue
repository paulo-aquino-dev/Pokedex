<template>
  <ul>
    <li v-for="pokemon in pokemons" :key="pokemon.nome">
      <img
        :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${get_pokemon_id(
          pokemon
        )}.png`"
        alt="pokemon.name"
        width="10%"
      />
      <h2 class="text-center">
        {{ pokemon.name }}
        <span class="title">#{{ get_pokemon_id(pokemon) }}</span>
      </h2>
    </li>
  </ul>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  components: {},
  data: () => ({
    pokemons: [],
  }),
  mounted() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151")
      .then((response) => {
        this.pokemons = response.data.results;
      });
  },
  methods: {
    get_pokemon_id(pokemon) {
      return Number(pokemon.url.split("/")[6]);
    },
  },
};
</script>
<style>

.title {
  padding-left: 200px;
}
</style>
