<script setup>
import { ref, onUnmounted } from 'vue'
const score = ref(0)
const activeHole = ref(null)
const isPlaying = ref(false)
let timer = null

const startGame = () => {
  score.value = 0
  isPlaying.value = true
  spawn()
}

const spawn = () => {
  if(!isPlaying.value) return
  activeHole.value = Math.floor(Math.random() * 6)
  timer = setTimeout(spawn, 800)
}

const whack = (idx) => {
  if(idx === activeHole.value) {
    score.value++
    activeHole.value = null
  }
}

onUnmounted(() => clearTimeout(timer))
</script>

<template>
  <div class="game">
    <h2>Score: {{ score }}</h2>
    <button v-if="!isPlaying" @click="startGame">Start Game</button>
    <div class="grid">
      <div v-for="i in 6" :key="i" class="hole" @click="whack(i-1)">
        <div v-if="activeHole === i-1" class="mole">🐹</div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.game { text-align: center; padding: 20px; }
.grid { display: grid; grid-template-columns: repeat(3, 100px); gap: 10px; justify-content: center; margin-top: 20px; }
.hole { width: 100px; height: 100px; background: #654321; border-radius: 50%; cursor: pointer; display: flex; align-items: center; justify-content: center; font-size: 40px; }
.mole { animation: pop 0.2s; }
@keyframes pop { from { transform: scale(0); } to { transform: scale(1); } }
</style>