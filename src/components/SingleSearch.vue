<template>
  <form id="form" @submit.prevent="onSubmit">
    <input type="text" id="pokemon" placeholder="Insert pokemon name" v-model="inputPokemon" />
  </form>
</template>

<script setup>
import { ref } from 'vue'

const single = ref('')
const inputPokemon = ref('')

const emit = defineEmits(['inputPokemon'])

const onSubmit = async () => {
  await fetch(`https://pokeapi.co/api/v2/pokemon/${pokemon.value}`)
    .then((response) => response.json())
    .then((data) => (single.value = data.name))
  emit('inputPokemon', single.value)
}
</script>
