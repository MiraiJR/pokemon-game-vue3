<template>
  <div class="screen">
    <h1>Congratulations</h1>
    <p>{{ Math.round(timer / 1000) }} seconds</p>
    <button class="btn" @click="startAgain()">Start again</button>
  </div>
</template>

<script>
export default {
  props: {
    onFirework: {
      type: Boolean,
      required: true,
    },
    timer: {
      type: Number,
      required: true,
    },
  },
  methods: {
    startAgain() {
      this.$emit("startAgain");
    },
  },
};
</script>

<style lang="css" scoped>
.screen {
  height: 100vh;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: var(--dark);
  color: var(--light);
}

h1 {
  font-size: 100px;
}

p {
  margin: 50px 0;
  font-size: 30px;
}
</style>
