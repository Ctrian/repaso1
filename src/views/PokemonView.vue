<template>
  <div>
    <div>
      <b>Puntaje:</b> {{ puntaje }} &nbsp; | &nbsp; <b>Intentos:</b> {{ intentos }}/5
    </div>
    <PokemonImage :pokemons="vectorPokemon" :mostrar="mostrar" />
    <button v-if="juegoTerminado" @click="reiniciarJuego">Juego nuevo</button>
    <button v-else @click="jugar">Jugar</button>
    <div v-if="mensaje" style="margin-top:10px;">{{ mensaje }}</div>
    <div v-if="mostrarMensajeFinal" :style="mensajeFinalStyle">{{ mensajeFinal }}</div>
  </div>
</template>

<script>
import PokemonImage from "@/components/PokemonImage.vue";

const POKEMONES_FIJOS = [
  { id: 1, nombre: "Bulbasaur" },
  { id: 4, nombre: "Charmander" },
  { id: 7, nombre: "Squirtle" },
  { id: 25, nombre: "Pikachu" },
  { id: 39, nombre: "Jigglypuff" }
];

function obtenerAleatorios(arr, n) {
  // Permite repetidos
  let resultado = [];
  for (let i = 0; i < n; i++) {
    resultado.push(arr[Math.floor(Math.random() * arr.length)]);
  }
  return resultado;
}

export default {
  components: { PokemonImage },
  data() {
    return {
      vectorPokemon: [],
      mostrar: false,
      puntaje: 0,
      intentos: 0,
      mensaje: "",
      mensajeFinal: "",
      mensajeFinalStyle: {},
      juegoTerminado: false,
      mostrarMensajeFinal: false
    };
  },
  methods: {
    jugar() {
      if (this.juegoTerminado) return;
      this.vectorPokemon = obtenerAleatorios(POKEMONES_FIJOS, 3);
      this.mostrar = true;
      this.intentos++;
      this.calcularPuntaje();
      this.verificarFinJuego();
    },
    calcularPuntaje() {
      const [a, b, c] = this.vectorPokemon.map(p => p.id);
      let puntos = 0;
      if (a === b && b === c) {
        puntos = 5;
        this.mensaje = "¡Felicidades! ¡Tres iguales!";
      } else if (a === b || a === c || b === c) {
        puntos = 2;
        this.mensaje = "¡Bien! ¡Dos iguales!";
      } else {
        puntos = 0;
        this.mensaje = "¡Sigue intentando!";
      }
      this.puntaje += puntos;
    },
    verificarFinJuego() {
      if (this.intentos >= 5) {
        this.juegoTerminado = true;
        if (this.puntaje >= 10) {
          this.mensajeFinal = "Felicitaciones has ganado un premio de $10.000,00";
          this.mensajeFinalStyle = { color: "blue", "font-weight": "bold" };
        } else {
          this.mensajeFinal = "Has utilizado tus 5 intentos. El juego ha terminado, inténtalo nuevamente";
          this.mensajeFinalStyle = { color: "red", "font-weight": "bold" };
        }
        this.mostrarMensajeFinal = true;
      }
    },
    reiniciarJuego() {
      this.vectorPokemon = obtenerAleatorios(POKEMONES_FIJOS, 3);
      this.mostrar = false;
      this.puntaje = 0;
      this.intentos = 0;
      this.mensaje = "";
      this.mensajeFinal = "";
      this.mensajeFinalStyle = {};
      this.juegoTerminado = false;
      this.mostrarMensajeFinal = false;
    }
  },
  mounted() {
    // Inicializa con placeholders
    this.vectorPokemon = obtenerAleatorios(POKEMONES_FIJOS, 3);
  }
};
</script>