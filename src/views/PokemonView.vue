<template>

<!-- texto inicial -->
<h1 class="texto-inicial" :style="{color: colorTextoInicial }">Seleccione el pokemon correcto</h1>

  <PokemonImage
    v-if="pokemonIdImagen && nombrePokemonImagen"
    v-bind:pokemon-id="pokemonIdImagen"
    v-bind:pokemon-nombre="nombrePokemonImagen"
    :mostrar-imagen="mostrarImagen"
  />
  <PokemonOptions
    v-bind:pokemons="vectorPokemon"
    @seleccionar-pokemon="mostrarNombre"
  />
  <div v-if="nombreSeleccionado" class="centrar">
    <h2>{{ mensaje }}</h2>
  </div>

  <div>
    <button @click="reiniciarJuego">Reiniciar juego</button>
  </div>
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
      nombreSeleccionado: "",
      pokemonIdImagen: null,
      nombrePokemonImagen: "",
      mostrarImagen: false,
      mensaje: "",
      colorTextoInicial: "black",
    };
  },
  methods: {
    async iniciarJuego() {
      const opciones = await obtenerOpcionesFachada(4);
      this.vectorPokemon = opciones;
      // Selecciona un índice aleatorio del arreglo de pokémon
      const indiceAleatorio = Math.floor(Math.random() * opciones.length);
      this.pokemonIdImagen = opciones[indiceAleatorio].id;
      this.nombrePokemonImagen = opciones[indiceAleatorio].nombre; // Guarda el nombre
      this.mostrarImagen = false;
      this.mensaje = "";
       this.nombreSeleccionado = "";
      this.colorTextoInicial = "black"; 
      console.log(this.vectorPokemon);
    },
    mostrarNombre(nombre) {
      this.nombreSeleccionado = nombre;
      // Revela la imagen solo si el nombre es correcto
      if (nombre === this.nombrePokemonImagen) {
        this.mostrarImagen = true;
        this.mensaje = "Felicitaciones, has   seleccionado la opción correcta";
        this.colorTextoInicial = "yellow";
      } else {
        this.mostrarImagen = true;
        this.mensaje = `Pokémon incorrecto, la respuesta es: ${this.nombrePokemonImagen}`;
        this.colorTextoInicial = "red"
      }
    },
    reiniciarJuego() {
      this.iniciarJuego();
    }
  },
  mounted() {
    this.iniciarJuego();
  },
};
</script>

<style>
.centrar {
  display: flex;
  justify-content: center;
  align-items: center;
}

h2 {
  background: rgb(108, 108, 241);
  border: solid;
  font-family: "Times New Roman", Times, serif;
  width: 250px;
}

.texto-inicial {
  color: black;
}

.texto-inicial {
  /* El color se controla por binding */
  transition: color 0.3s;
}

</style>
