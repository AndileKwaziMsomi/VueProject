<template>
  <div class="block" v-if="showBlock" @click="stopTimer"> Click
  </div>
</template>

<script>
export default {
  props: ['delay'],
  data() {
    return {
      showBlock: false, // Initially false so the block doesn't appear twice
      startTime: null,
      reactionTime: 0
    }
  },
  mounted() {
    setTimeout(() => {
      this.showBlock = true; // Show the block after the delay
      this.startTimer();  
    }, this.delay);
  },
  methods: {
    startTimer() {
      this.startTime = Date.now();
    },
    stopTimer() {
      const endTime = Date.now();
      this.reactionTime = endTime - this.startTime;
      this.showBlock = false; // Hide the block after the click
      this.$emit('blockClicked', this.reactionTime);
      this.$emit('blockedHidden');
    }
   
  }
}
</script>

<style>
.block {
  width: 400px;
  border-radius: 35px;
  background: grey;
  color: white;
  text-align: center;
  margin: 40px auto;
  padding: 100px 0;
  cursor: pointer;
}
</style>
