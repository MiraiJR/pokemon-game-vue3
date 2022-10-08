<template>
  <div class="screen">
    <h1 class="screen__title">Interact Component here</h1>
    <div
      class="screen__inner"
      :style="{
        width: `${
          ((((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4 +
            16) *
          Math.sqrt(cardsContext.length)
        }px`,
      }"
    >
      <card-flip
        v-for="(card, index) in cardsContext"
        :key="index"
        :ref="`card-${index}`"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        :cardsContext="cardsContext"
        @onFlip="checkRule($event)"
      />
    </div>

    <button class="btn" @click="onBackToMain">Back</button>
  </div>
</template>

<script>
import CardFlip from "./CardPokemon.vue";
export default {
  props: {
    cardsContext: {
      type: Array,
      default: () => {
        return [];
      },
    },
  },
  components: {
    CardFlip,
  },
  data() {
    return {
      rules: [],
    };
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) return false;

      if (this.rules.length < 2) {
        this.rules.push(card);
      }

      if (this.rules.length === 2) {
        if (this.rules[0].value === this.rules[1].value) {
          // add class 'disabled'
          this.$refs[`card-${this.rules[0].index}`][0].holdFlipFrontCard();
          this.$refs[`card-${this.rules[1].index}`][0].holdFlipFrontCard();

          //reset rules to []
          this.rules = [];

          const disabledElements = document.querySelectorAll(
            ".screen .card.disabled"
          );
          if (
            disabledElements &&
            disabledElements.length === this.cardsContext.length - 2
          ) {
            setTimeout(() => {
              this.$emit("onFinish");
            }, 1000);
          }
        } else {
          setTimeout(() => {
            // close different card
            this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
            this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();

            // reset rules to []
            this.rules = [];
          }, 800);
        }
      } else {
        return false;
      }
    },

    onBackToMain() {
      this.$emit("onBack");
    },
  },
};
</script>

<style lang="css" scoped>
.screen {
  width: 100%;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.screen__title {
  width: 100%;
  text-align: center;
  font-size: 50px;
}

.screen__inner {
  width: 424px;
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
