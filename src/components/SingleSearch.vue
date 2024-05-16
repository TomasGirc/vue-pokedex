<template>
  <form id="form" @submit.prevent="onSubmit">
    <input
      class="focus:ring-2 focus:ring-blue-500 focus:outline-none appearance-none w-full text-sm leading-6 text-slate-900 placeholder-slate-400 rounded-md py-2 pl-10 ring-1 ring-slate-200 shadow-sm"
      type="text"
      id="pokemon"
      placeholder="Insert pokemon name"
      v-model="inputPokemon"
    />
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
