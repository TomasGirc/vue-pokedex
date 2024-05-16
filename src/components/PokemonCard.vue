<template>
  <div v-if="loaded">
    <img
      v-if="pokemon.sprites"
      :src="`${pokemon.sprites.front_default}`"
      alt=""
      class="h-100 w-100 rounded-full"
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
import { onMounted, onUpdated, ref } from 'vue'

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
.attacker {
  background: $attackRed;
  border: 1px solid $attackRed;
  border-radius: 6px;
  box-shadow: rgba(0, 0, 0, 0.1) 1px 2px 4px;
  box-sizing: border-box;
  color: #ffffff;
  cursor: pointer;
  display: inline-block;
  font-family: nunito, roboto, proxima-nova, 'proxima nova', sans-serif;
  font-size: 16px;
  font-weight: 800;
  line-height: 16px;
  min-height: 40px;
  outline: 0;
  padding: 12px 14px;
  text-align: center;
  text-rendering: geometricprecision;
  text-transform: none;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  vertical-align: middle;
}

.attacker:hover,
.attacker:active {
  background-color: initial;
  background-position: 0 0;
  color: $attackRed;
}

.defender {
  background: $defendGreen;
  border: 1px solid $defendGreen;
  border-radius: 6px;
  box-shadow: rgba(0, 0, 0, 0.1) 1px 2px 4px;
  box-sizing: border-box;
  color: #ffffff;
  cursor: pointer;
  display: inline-block;
  font-family: nunito, roboto, proxima-nova, 'proxima nova', sans-serif;
  font-size: 16px;
  font-weight: 800;
  line-height: 16px;
  min-height: 40px;
  outline: 0;
  padding: 12px 14px;
  text-align: center;
  text-rendering: geometricprecision;
  text-transform: none;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  vertical-align: middle;
}

.defender:hover,
.defender:active {
  background-color: initial;
  background-position: 0 0;
  color: $defendGreen;
}

.attacker:active,
.defender:active {
  opacity: 0.5;
}
</style>
