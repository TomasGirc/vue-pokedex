<template>
  <div>
    <p>Attacker : {{ props.attacker.name }}</p>
    <img v-if="props.attacker.sprites" :src="`${props.attacker.sprites.front_default}`" />
  </div>
  <div>
    <p>Defender : {{ props.defender.name }}</p>
    <img v-if="props.defender.sprites" :src="`${props.defender.sprites.front_default}`" />
  </div>
</template>

<script setup>
import { defineProps } from 'vue'
const props = defineProps({
  attacker: {
    type: Object,
    required: true
  },
  defender: {
    type: Object,
    required: true
  }
})
</script>
