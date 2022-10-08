<template>
  <div class="screen">
    <img src="../assets/android-chrome-512x512.png" alt="" />
    <h1 class="screen__title">POKEMON - GAME</h1>
    <h3 class="screen__title--sub">Select mode to start game</h3>
    <div class="actions">
      <button @click="onStart(16)">
        <span>4x4</span>
        <span>Easy</span>
      </button>
      <button @click="onStart(36)">
        <span>6x6</span>
        <span>Normal</span>
      </button>
      <button @click="onStart(64)">
        <span>8x8</span>
        <span>Hard</span>
      </button>
      <button @click="onStart(100)">
        <span>10x10</span>
        <span>Super hard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStart(totalOfBlocks) {
      this.$emit("onStart", { totalOfBlocks });
    },
  },
};
</script>

<style lang="css" scoped>
.screen {
  width: 100%;
  height: inherit;
  margin: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: white;
  background-color: var(--dark);
}

img {
  width: 300px;
  height: 300px;
}

.screen__title {
  font-size: 50px;
  text-shadow: 0 0 10px #fff, 0 0 20px #fff, 0 0 30px #e60073, 0 0 40px #e60073,
    0 0 50px #e60073, 0 0 60px #e60073, 0 0 70px #e60073;
  margin-bottom: 20px;
}

.actions {
  display: flex;
}

.actions button {
  width: 150px;
  height: 150px;
  color: var(--light);
  font-size: 25px;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: var(--dark);
  border-radius: 1rem;
  transition: all 0.3s linear;
  cursor: pointer;
  margin: 30px;
}

.actions button:hover {
  background-color: var(--light);
  color: var(--dark);
}

span {
  font-family: var(--font);
}
</style>
