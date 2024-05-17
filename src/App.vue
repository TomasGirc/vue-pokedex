<template>
  <TailwindHeader />
  <div class="wrap">
    <div class="sticky w-1/5 invisible lg:visible lside">
      <p class="text-lg">{{ capitalizeFirstLetter(pokemonA.name) }}</p>
      <div class="pokemonSideImage" :style="backgroundPokemon(true)"></div>
    </div>

    <div class="main w-5/5 lg:w-3/5">
      <RouterView />
    </div>
    <div class="sticky w-1/5 invisible lg:visible rside">
      <p class="text-lg">{{ capitalizeFirstLetter(pokemonD.name) }}</p>
      <div class="pokemonSideImage" :style="backgroundPokemon(false)"></div>
    </div>
  </div>
</template>

<script setup lang="ts">
import TailwindHeader from './components/TailwindHeader.vue'
import { onMounted, ref } from 'vue'

type Pokemon = {
  name: string
  id: number
}

const pokemonA = ref<Pokemon>({ name: '', id: 0 })
const pokemonD = ref<Pokemon>({ name: '', id: 0 })

function capitalizeFirstLetter(str: string) {
  return str.charAt(0).toUpperCase() + str.slice(1)
}

const randomNumber = () => {
  return Math.floor(Math.random() * 1025)
}

const pokemonFetchAttack = () => {
  fetch(`https://pokeapi.co/api/v2/pokemon/${randomNumber()}`)
    .then((response) => response.json())
    .then((data) => (pokemonA.value = data))
}
const pokemonFetchDefend = () => {
  fetch(`https://pokeapi.co/api/v2/pokemon/${randomNumber()}`)
    .then((response) => response.json())
    .then((data) => (pokemonD.value = data))
}

const backgroundPokemon = (attacker: boolean) => {
  return {
    'background-image': `url('https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/home/${attacker ? pokemonA.value.id : pokemonD.value.id}.png')`
  }
}
onMounted(() => {
  pokemonFetchAttack()
  pokemonFetchDefend()
})
</script>

<style lang="scss" scoped>
*,
*:before,
*:after {
  box-sizing: inherit;
}
html,
body {
  margin: 0;
  padding: 0;
}

.wrap {
  display: flex;
  min-height: 100vh;
  align-items: flex-start;
}
.sticky {
  position: sticky;
  top: 0;
  border: 2px solid $attackRed;
}
.main {
  flex: 1 0 0;
  border: 10px solid $color-tertiary;
  padding: 10px;
}

.lside,
.rside {
  .pokemonSideImage {
    min-height: 100vh;
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center;
  }
  p {
    color: $color-black;
    font-family: 'Pokemon Solid', sans-serif;
    // -webkit-text-stroke: 1px $color-gold;
    font-size: 32px;
    padding-top: 12px;
    margin-left: auto;
    margin-right: auto;
    left: 0;
    right: 0;
    text-align: center;
    @include stroke(1, $color-gold);
  }
}

.lside {
  background-color: $attackRed;
}
.rside {
  background-color: $defendGreen;
}
</style>
