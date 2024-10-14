<template>
  <div>
    <h1>Hey, Let's play a game</h1>
    <button @click="start" :disabled="isPlaying">Press Play</button>
    <div>
      <button @click="resetGame" :disabled="!isPlaying">Reset</button>
    </div>
    <!-- Block only appears if the game is playing -->
    <block v-if="isPlaying" :delay="delay" @blockHidden="endGame" />
  </div>
</template>

<script>
import Block from './components/Block.vue'

export default {
  name: 'App',
  components: { Block },
  data() {
    return {
      isPlaying: false,
      delay: null
    };
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
    },
    resetGame() {
      this.isPlaying = false;  // Stop the game
      this.delay = null;       // Reset the delay
    },
    endGame() {
      this.isPlaying = false;  // End the game when block is hidden
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
button {
  margin-top: 20px;
  padding: 10px 20px;
  border: none;
  background-color: #58626d;
  color: white;
  border-radius: 5px;
  cursor: pointer;
}
button:disabled {
  background-color: #b0b0b0;
}
</style>
