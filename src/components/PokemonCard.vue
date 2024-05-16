<template>
  <div v-if="loaded">
    <img
      v-if="pokemon.sprites"
      :src="`${pokemon.sprites.front_default}`"
      alt=""
      class="h-100 w-100 rounded-ful"
    />
    <h3 class="text-sm font-medium text-gray-900">{{ pokemon.name }}</h3>
    <div v-for="stats in pokemon.stats" :key="stats.stat.name">
      <p class="text-sm text-gray-500">{{ stats.stat.name }} : {{ stats.base_stat }}</p>
    </div>
    <button @click="selectAttacker(pokemon)" class="attacker">Attacker</button>
    <button @click="selectDefender(pokemon)" class="defender">Defender</button>
  </div>
</template>

<script setup>
import { defineProps, onMounted, onUpdated, ref } from 'vue'

const props = defineProps({
  name: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['selectedAttacker', 'selectedDefender'])

const pokemon = ref({})
const loaded = ref(false)

const fetchPokemon = () => {
  fetch(`https://pokeapi.co/api/v2/pokemon/${props.name}`)
    .then((response) => response.json())
    .then((dataPokemon) => (pokemon.value = dataPokemon))
    .finally((loaded.value = true))
}

const selectAttacker = (data) => {
  emit('selectedAttacker', data)
}

const selectDefender = (data) => {
  emit('selectedDefender', data)
}

onMounted(() => {
  props.name && fetchPokemon()
})
onUpdated(() => {
  props.name !== pokemon.value.name && fetchPokemon()
})
</script>

<style lang="scss">
$attackRed: red;
$defendGreen: green;

.attacker {
  background-color: $attackRed;
}

.defender {
  background-color: $defendGreen;
}
</style>
