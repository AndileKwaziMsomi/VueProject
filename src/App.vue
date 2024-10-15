<template>
  <div>
    <h1>Hey, Let's play a game</h1>
    <button @click="start" :disabled="isPlaying">Press Play</button>
    <div>
      <button @click="resetGame" :disabled="!isPlaying">Reset</button>
    </div>
    <!-- Render block when playing and pass delay -->
    <block v-if="isPlaying" :delay="delay" @blockClicked="endGame" />
    <!-- Show results when the game is finished -->
    <Results v-if="showResults" :score="score" />
  </div>
</template>

<script>
import Block from './components/Block.vue'
import Results from './components/Results.vue';

export default {
  name: 'App',
  components: { Block, Results },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      startTime: null,
      showResults: false
    };
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000; // Random delay
      this.isPlaying = true;
      this.showResults = false;
      setTimeout(() => {
        this.startTime = new Date().getTime(); // Record the start time when block appears
      }, this.delay);
    },
    resetGame() {
      this.isPlaying = false;  
      this.delay = null;
      this.startTime = null;
      this.showResults = false;
    },
    endGame() {
      const endTime = new Date().getTime(); // Record the time user clicks block
      this.score = endTime - this.startTime; // Calculate the reaction time
      this.isPlaying = false;
      this.showResults = true;
    }
  }
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

button {
  margin-top: 50px;
  padding: 10px 20px;
  border: none;
  background-color: #58626d;
  color: white;
  border-radius: 5px;
  cursor: pointer;
  position: relative;
  
}

button:disabled {
  background-color: #b0b0b0;
}
</style>
