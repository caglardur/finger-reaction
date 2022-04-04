<template>
  <div class="app" @click.self="errorHandler">
    <h1>finger timer</h1>
    <button @click="start" :disabled="isPlaying">play</button>
    <ClickBlok v-if="isPlaying" :delay="delay" @end="endGame" />
    <ResultBlok v-if="showResults" :score="score" />
    <p v-if="error">too fast...</p>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue"
import ClickBlok from "./components/ClickBlok.vue"
import ResultBlok from "./components/ResultBlok.vue"

export default defineComponent({
  name: "App",
  components: { ClickBlok, ResultBlok },
  setup() {
    const isPlaying = ref(false)
    const delay = ref<number | null>(null)
    const score = ref<number | null>(null)
    const showResults = ref(false)
    const error = ref(false)
    return { isPlaying, delay, score, showResults, error }
  },

  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = true
      this.showResults = false
      this.error = false
    },
    endGame(reactionTime: number) {
      this.score = reactionTime
      this.isPlaying = false
      this.showResults = true
      this.error = false
    },
    errorHandler() {
      if (this.isPlaying) {
        this.error = true
        this.isPlaying = false
      }
    }
  }
})
</script>

<style>
.app {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  text-align: center;
  color: #444;
  margin-top: 60px;
  height: 100vh;
}
button {
  background: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}
button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
