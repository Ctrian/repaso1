<template>
  <div class="options-container">
    <ul>
      <li
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        @click="$emit('seleccionar-pokemon', pokemon.nombre)"
      >
        {{ pokemon.nombre }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    pokemons: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style>
.options-container {
  display: flex;
  justify-content: center;
}

ul {
  list-style-type: none;
}

li {
  background: #46c37a;
  border-radius: 5px;
  border: 1px solid skyblue;
  cursor: pointer;
  margin-bottom: 10px;
  width: 150px;
}

li:hover {
  background: lemonchiffon;
}
</style>
