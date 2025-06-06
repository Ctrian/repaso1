<template>
  <div class="image-container">
    <!-- objetivo: mostrar la imagen/es -->

    <img
      :class= "{ ocultar: !mostrarImagen }"
      v-bind:src="imagenFuente"
      alt="No se puede renderizar la imagen del pokemon"
    />

  </div>
</template>

<script>
export default {
  props: {
    pokemonId: {
      type: Number,
      required: true,
    },
    pokemonNombre: {
      type: String,
      required: false,
      default: "",
    },
    mostrarImagen: {
      type: Boolean,
      required: true,
      default: false,
    },
  },
  computed: {
    imagenFuente() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`;
    },
  },
  data() {
    return {
      mostrar: this.mostrarImagen,
    };
  },mounted() {
    console.log(`Nombre: ${this.pokemonNombre}, ID: ${this.pokemonId}`);
  }
};
</script>

<style>
img {
    height: 200px;
    /* atras de la imagen con la clase ocultar */
    position: absolute;
    right: 35%;
}

.ocultar {
    filter: brightness(0);
}

.image-container {
    height: 200px;
}
</style>
