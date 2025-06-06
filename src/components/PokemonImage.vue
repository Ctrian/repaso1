<template>
  <div class="image-container">
    <div class="imagenes">
      <div v-for="pokemon in pokemons" :key="pokemon.id" class="pokemon-card">
        <img
          :src="
            mostrar ? getPokemonUrl(pokemon.id) : 'https://placehold.co/250x250'
          "
          alt="Imagen del pokemon"
          class="pokemon-img"
        />

        <div class="pokemon-nombre">
          {{ pokemon.nombre }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    pokemons: {
      type: Array,
      required: true,
    },
    mostrar: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      mostrar: false,
    };
  },
  methods: {
    getPokemonUrl(id) {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${id}.svg`;
    },
  },
};
</script>

<style>
.imagenes {
  display: flex;
  flex-direction: row;
  gap: 20px;
  justify-content: center;
  align-items: flex-start;
  padding-bottom: 20px;
}
.pokemon-card {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.pokemon-img {
  height: 200px;
  width: 200px;
  object-fit: contain;
}
.image-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
