<template>
  <div>
    <Realistic :pokemon="pokemonA" />
    <draggableComponent
      v-model="moveOptions2"
      tag="div"
      @start="test()"
      group="moves"
      item-key="id"
      @change="moveOptions2.splice(1), onChange"
      @click="removeList"
    >
      <template #item="{ element: skill }">
        <div itemKey="skill.id" class="drag w-1/5">
          <div class="container">
            <div class="wrapper">
              <div class="banner-image"></div>
              <h1>{{ skill.name }}</h1>
            </div>
            <div class="button-wrapper">
              <button class="btn outline">DETAILS</button>
              <button class="btn fill">BUY NOW</button>
            </div>
          </div>
        </div>
      </template>
      <template v-slot:footer>
        <div class="btn-group list-group-item" role="group" aria-label="Basic example" key="footer">
          <button class="btn btn-secondary">Add</button>
        </div>
      </template>
    </draggableComponent>

    <draggableComponent
      class="flex"
      v-model="moveOptions"
      tag="div"
      @start="test()"
      item-key="id"
      @change="onChange"
      :group="{ name: 'moves', pull: 'clone', put: false }"
    >
      <template #item="{ element: skill }">
        <div itemKey="skill.id" class="drag w-1/5">
          <div class="container">
            <div class="wrapper">
              <div class="banner-image"></div>
              <h1>{{ skill.name }}</h1>
              <p>
                Lorem ipsum dolor sit amet, <br />
                consectetur adipiscing elit.
              </p>
            </div>
            <div class="button-wrapper">
              <button class="btn outline">DETAILS</button>
              <button class="btn fill">BUY NOW</button>
            </div>
          </div>
        </div>
      </template>
    </draggableComponent>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
import draggableComponent from 'vuedraggable'
import Realistic from '../components/RealisticCards.vue'

type Pokemon = {
  name: string
  id: number
}

// Applouse meter??
// Order and order shuffle
// Stars - gives points, prevents jamming and conditions
// Repeated use penalty
// Status effect
// Combo meter
// 5 card draw | discard one or more for energy | spend energy to use other cards in show

type Ability = {
  id: number
  name: string
  power: number
  type: combatTypes
  pp: number
  appeal: number
  jam: number
  accuracy: number | null
  effect: string // make to different object
  combo: {
    normal: {
      nameBefore: string
      idBefore: number
    }
    super: {
      nameBefore: string
      idBefore: number
    } | null
  }
  penalty: number
}[]

type combatTypes = 'cool' | 'beauty' | 'cute' | 'smart' | 'tough'

const pokemonA = ref<Pokemon>({ name: '', id: 0 })
const pokemonD = ref<Pokemon>({ name: '', id: 0 })

const moveOptions = ref<Ability>([
  {
    id: 0,
    name: 'First',
    power: 0,
    type: 'cool',
    pp: 0,
    appeal: 0,
    jam: 0,
    accuracy: 0,
    effect: '', // make to different object
    combo: {
      normal: {
        nameBefore: '',
        idBefore: 0
      },
      super: {
        nameBefore: '',
        idBefore: 0
      }
    },
    penalty: 0
  },
  {
    id: 2,
    name: 'Second',
    power: 0,
    type: 'cool',
    pp: 0,
    appeal: 0,
    jam: 0,
    accuracy: 0,
    effect: '', // make to different object
    combo: {
      normal: {
        nameBefore: '',
        idBefore: 0
      },
      super: {
        nameBefore: '',
        idBefore: 0
      }
    },
    penalty: 0
  },
  {
    id: 1,
    name: 'Third',
    power: 0,
    type: 'cool',
    pp: 0,
    appeal: 0,
    jam: 0,
    accuracy: 0,
    effect: '', // make to different object
    combo: {
      normal: {
        nameBefore: '',
        idBefore: 0
      },
      super: {
        nameBefore: '',
        idBefore: 0
      }
    },
    penalty: 0
  }
])

const moveOptions2 = ref<Ability>([
  {
    id: 4,
    name: 'Third',
    power: 0,
    type: 'cool',
    pp: 0,
    appeal: 0,
    jam: 0,
    accuracy: 0,
    effect: '', // make to different object
    combo: {
      normal: {
        nameBefore: '',
        idBefore: 0
      },
      super: {
        nameBefore: '',
        idBefore: 0
      }
    },
    penalty: 0
  }
])

const pokemonFetchAttack = () => {
  fetch(`https://pokeapi.co/api/v2/pokemon/${25}`)
    .then((response) => response.json())
    .then((data) => (pokemonA.value = data))
}
const pokemonFetchDefend = () => {
  fetch(`https://pokeapi.co/api/v2/pokemon/${6}`)
    .then((response) => response.json())
    .then((data) => (pokemonD.value = data))
}

const test = () => {
  console.warn('Started')
}

const onChange = () => {
  console.warn('Trigger')
}
const removeList = () => {
  moveOptions2.value = []
}

onMounted(() => {
  pokemonFetchAttack()
  pokemonFetchDefend()
})
</script>

<style scoped lang="scss">
.drag {
  cursor: pointer;
}

.container {
  backdrop-filter: blur(16px) saturate(180%);
  -webkit-backdrop-filter: blur(16px) saturate(180%);
  background-color: rgba(17, 25, 40, 0.25);
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.125);
  padding: 38px;
  filter: drop-shadow(0 30px 10px rgba(0, 0, 0, 0.125));
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
}

.wrapper {
  width: 100%;
  height: 100%;
}

.banner-image {
  background-image: url(https://images.unsplash.com/photo-1641326201918-3cafc641038e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1887&q=80);
  background-position: center;
  background-size: cover;
  height: 300px;
  width: 100%;
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.255);
}

h1 {
  font-family: 'Righteous', sans-serif;
  color: rgba(255, 255, 255, 0.98);
  text-transform: uppercase;
  font-size: 2.4rem;
}

p {
  color: #fff;
  font-family: 'Lato', sans-serif;
  text-align: center;
  font-size: 0.8rem;
  line-height: 150%;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.button-wrapper {
  margin-top: 18px;
}

.btn {
  border: none;
  padding: 12px 24px;
  border-radius: 24px;
  font-size: 12px;
  font-size: 0.8rem;
  letter-spacing: 2px;
  cursor: pointer;
}

.btn + .btn {
  margin-left: 10px;
}

.outline {
  background: transparent;
  color: rgba(0, 212, 255, 0.9);
  border: 1px solid rgba(0, 212, 255, 0.6);
  transition: all 0.3s ease;
}

.outline:hover {
  transform: scale(1.125);
  color: rgba(255, 255, 255, 0.9);
  border-color: rgba(255, 255, 255, 0.9);
  transition: all 0.3s ease;
}

.fill {
  background: rgba(0, 212, 255, 0.9);
  color: rgba(255, 255, 255, 0.95);
  filter: drop-shadow(0);
  font-weight: bold;
  transition: all 0.3s ease;
}

.fill:hover {
  transform: scale(1.125);
  border-color: rgba(255, 255, 255, 0.9);
  filter: drop-shadow(0 10px 5px rgba(0, 0, 0, 0.125));
  transition: all 0.3s ease;
}
</style>
