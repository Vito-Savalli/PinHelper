<template>
  <div>
    <button @click="pauseChrono">CAR</button>
    <button @click="restartChrono">Relo</button>
  </div>
  <div>
    <div class="chrono">{{ elapsedSeconds }}</div>
    <button @click="startChrono">Play</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      lastStartTime: null,
      accumulatedTime: 0,
      timerInterval: null,
    };
  },
  computed: {
    elapsedSeconds() {
      const seconds = Math.floor(this.accumulatedTime / 1000);
      return `${String(Math.floor(seconds / 60)).padStart(2, "0")}:${String(
        seconds % 60
      ).padStart(2, "0")}`;
    },
  },
  methods: {
    updateChrono() {
      this.accumulatedTime += Date.now() - this.lastStartTime;
      this.lastStartTime = Date.now();
    },
    startChrono() {
      if (this.timerInterval) return; // If already running, don't start again
      this.lastStartTime = Date.now();
      this.timerInterval = setInterval(this.updateChrono, 1000);
    },
    pauseChrono() {
      clearInterval(this.timerInterval);
      this.timerInterval = null;
      this.updateChrono(); // Update accumulated time upon pausing
    },
    restartChrono() {
      this.pauseChrono();
      this.accumulatedTime = 0;
    },
  },
};
</script>

<style scoped>
.chrono {
  /* Add your styles for the chronometer display here */
  font-size: 14px;
}

div {
  display: flex;
  flex-direction: column;
}
</style>
