<template>
  <div id="body" @Click.self="isCheating">
    <h1>Reaction Timer Game</h1>
    <button @click="start" :disabled="isPlaying">Play</button>
    <Block v-if="isPlaying" :delay="delay" @end="endGame"/>
    <Results v-if="showResults" :score="score"/>
    <p>{{ cheatMsg }}</p>
  </div>
</template>

<script>
import Block from '@/components/Block.vue'
import Results from '@/components/Results.vue'

export default {
  name: 'App',
  components: {Block, Results},
  data() {
    return {
      isPlaying: false,
      delay: null,
      scrore: null,
      showResults: false,
      cheatMsg: null
    }
  },
  methods: {
    start() {
      this.delay = 1000 + Math.random() * 3000
      this.isPlaying = true
      this.showResults = false
    },
    endGame(reactionTime) {
      this.score = reactionTime
      this.isPlaying = false
      this.showResults = true
    },
    isCheating() {
        this.isPlaying = false
        this.showResults = false
        this.delay = null
        this.cheatMsg = 'Please click on the green block.'
        setTimeout(() => {
          this.cheatMsg = ''
          }, 2000)
    }
  }
}
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #444;
    margin-top: 60px;
  }
  #body{
    height: 500px;
  }
  button {
    background: #0faf87;
    color: #fff;
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
