<template>
  <div v-if="pokedex">
    <CombatComponent v-if="attacker || defender" :attacker="attacker" :defender="defender" />
    <div>Pokemon count : {{ pokedex.count }}</div>
    <SingleSearch @inputPokemon="handleInput"></SingleSearch>
    {{ single }}
    <PokemonCard
      :name="single"
      @selectedAttacker="pokemonAttacker"
      @selectedDefender="pokemonDefender"
    />

    <button @click="pageForward(false)">Back</button>
    <button @click="pageForward(true)">Next</button>

    <div class="flex flex-wrap">
      <div v-for="pokemon in pokedex.results" :key="pokemon.name" class="w-1/2">
        <PokemonCard
          :name="pokemon.name"
          @selectedAttacker="pokemonAttacker"
          @selectedDefender="pokemonDefender"
        />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
import PokemonCard from './PokemonCard.vue'
import CombatComponent from './CombatComponent.vue'
import SingleSearch from './SingleSearch.vue'

type Pokedex = {
  count: Number
  results: Object
}

const offset = ref(0)
const pokedex = ref<Pokedex | null>(null)
const single = ref('')
const attacker = ref({})
const defender = ref({})

const pokemonFetch = () => {
  fetch(`https://pokeapi.co/api/v2/pokemon?offset=${offset.value}&limit=9`)
    .then((response) => response.json())
    .then((data) => (pokedex.value = data))
}

const pokemonAttacker = (data: string) => {
  attacker.value = data
}
const pokemonDefender = (data: string) => {
  defender.value = data
}

const handleInput = (data: string) => {
  single.value = data
}

const pageForward = (forward: boolean) => {
  forward
    ? ((offset.value += 10), pokemonFetch())
    : offset.value >= 10 && ((offset.value -= 10), pokemonFetch())
}

onMounted(() => {
  pokemonFetch()
})
</script>
