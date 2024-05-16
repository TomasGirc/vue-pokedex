<template>
  <div class="flex">
    <div class="w-1/2">
      <p>Attacker : {{ props.attacker.name }}</p>
      <img v-if="props.attacker.sprites" :src="`${props.attacker.sprites.front_default}`" />
    </div>
    <div class="w-1/2">
      <p>Defender : {{ props.defender.name }}</p>
      <img v-if="props.defender.sprites" :src="`${props.defender.sprites.front_default}`" />
    </div>
  </div>
</template>

<script setup>
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
