<template>
  <div id="sand" class="sand-container">
    <b-card
      class="sand-card"
      :class="{ aho: isAho }"
      :border-variant="isAho ? 'warning' : ''"
      :header-bg-variant="isAho ? 'warning' : ''"
    >
      <template #header>
        <h4 class="sand-card-header">
          <span v-if="isAho" class="sand-card-face">😜</span>
          <span v-else class="sand-card-face">🙁</span>
        </h4>
      </template>
      <b-card-body class="sand-card-body">
        <b-card-title class="sand-card-number">{{
          counter
        }}</b-card-title>
        <b-card-sub-title class="sand-card-title"
          >三度カウンター</b-card-sub-title
        >
        <b-card-text class="sand-card-text">
          3の倍数、または3が含まれているとアホになります。
        </b-card-text>
        <b-button variant="secondary" @click="resetCounter">リセット</b-button>
      </b-card-body>
    </b-card>
  </div>
</template>
<script>
export default {
  data() {
    return {
      counter: 0,
      timeoutId: null,
    };
  },
  computed: {
    isAho() {
      return this.contains3(this.counter) || this.divide3(this.counter);
    },
  },
  methods: {
    contains3(value) {
      return /3/.test(value);
    },
    divide3(value) {
      return value / 3 === Math.round(value / 3) && value !== 0;
    },
    resetCounter() {
      this.counter = 0;
      clearTimeout(this.timeoutId);
      this.setTimeoutCounter();
    },
    setTimeoutCounter() {
      this.timeoutId = setTimeout(this.incrementCounter, 1000);
    },
    incrementCounter() {
      this.counter++;
      this.setTimeoutCounter();
    },
    onReset() {
      this.counter = 0;
    },
  },
  created() {
    this.setTimeoutCounter();
  },
};
</script>
<style lang="scss" scoped>
.sand-container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}
.sand-card-header {
  margin-bottom: 0;
  font-size: 5.5rem;
  text-align: center;
}
.sand-card-number{
    font-size: 7rem;
    .aho & {
        color: #C00;
    }
}
.sand-card-number,
.sand-card-title{
    text-align: center;
}
.sand-card-title{
    margin-bottom: 1rem;
}
</style>