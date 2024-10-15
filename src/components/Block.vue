<template>
  <div class="block" v-if="showBlock" @click="stopTimer"> Quickly Press here
  </div>
</template>

<script>
export default {
  props: ['delay'],
  data() {
    return {
      showBlock: false, 
      startTime: null,
      reactionTime: 0
      
    }
  },
  mounted() {
    setTimeout(() => {
      this.showBlock = true;
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
      this.showBlock = false;
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
