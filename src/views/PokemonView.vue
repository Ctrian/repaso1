<template>
  <PokemonImage :pokemons="vectorPokemon" :mostrar="mostrar" />
   <button @click="mostrar = !mostrar">Jugar</button>
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
      mostrar: false,
    };
  },
  methods: {
    async iniciarJuego() {
      const opciones = await obtenerOpcionesFachada(3);
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