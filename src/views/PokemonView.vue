<template>
  <PokemonImage v-bind:pokemon-id="384" :mostrar-imagen="true" />
  <PokemonOptions v-bind:pokemons="vectorPokemon"/>
</template>

<script>
import PokemonImage from "@/components/PokemonImage.vue";
import PokemonOptions from "@/components/PokemonOptions.vue";

import { obtenerOpcionesFachada } from "@/clients/PokemonClient";

export default {
  components: {
    PokemonImage,
    PokemonOptions,
  },
  data() {
    return {
      vectorPokemon: [],
    };
  },
  methods: {
    async iniciarJuego() {
      const opciones = await obtenerOpcionesFachada(5);
      this.vectorPokemon = opciones;
      console.log(this.vectorPokemon);
    },
  },
  mounted() {
    this.iniciarJuego();
  },
};
</script>

<style></style>
