<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
    @onFinish="onGetResult"
    @onBack="onBackToMain"
  />
  <result-screen
    v-if="statusMatch === 'result'"
    :timer="timer"
    :onFireWork="onFirework"
    @startAgain="onStartAgain"
  />
  <p class="copyright">
    This game owned by RHP Team and I recoded -
    <a href="https://www.facebook.com/TruongVanHao111">view here</a>
  </p>
  <audio id="audioPokemon" controls autoplay loop>
    <source
      src="https://vgmsite.com/soundtracks/pokemon-gameboy-sound-collection/vvdpydwp/101-opening.mp3"
      type="audio/mpeg"
    />
  </audio>
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import { shuffled } from "./utils/Array";
import ResultScreen from "./components/ResultScreen.vue";
// import CopyRightScreenVue from "./components/CopyRightScreen.vue";
export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
    // CopyRightScreenVue,
  },
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
        endedAt: null,
      },
      statusMatch: "default",
      timer: 0,
      onFirework: true,
    };
  },
  methods: {
    onHandleBeforeStart(config) {
      console.log("Running handle before start, ", config.totalOfBlocks);
      this.settings.totalOfBlocks = config.totalOfBlocks;

      const firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );

      const secondCards = [...firstCards]; //clone shadow
      const cards = [...firstCards, ...secondCards];

      this.settings.cardsContext = shuffled(shuffled(shuffled(cards)));
      this.settings.startedAt = new Date().getTime();

      // data ready
      this.statusMatch = "match";
    },

    onGetResult() {
      // get timer
      this.timer = new Date().getTime() - this.settings.startedAt;

      //switch to result component
      this.statusMatch = "result";
    },

    onStartAgain() {
      this.statusMatch = "default";
    },

    onBackToMain() {
      this.statusMatch = "default";
    },
  },
};
</script>

<style lang="css" scoped>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 1.5rem;
  color: var(--light);
  z-index: 3;
  font-size: 1.5rem;
}
.copyright a {
  color: #f4dc26;
}

audio {
  display: none;
}
</style>
