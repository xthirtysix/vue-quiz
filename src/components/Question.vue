<template>
  <b-card
    tag="question"
    style="max-width: 40rem; margin: 0 auto;"
    class="mb-2"
  >
    <template v-slot:header>
      <h3>{{ question }}</h3>
    </template>

    <ul>
      <li :key="i" v-for="(variant, i) in variants">
        <b-button
          href="#"
          class="variant"
          variant="primary">
          {{variant.value}}
        </b-button>
      </li>
    </ul>
  </b-card>
</template>

<script>
const MATH_ADD = 0;
const MATH_EXCLUDE = 1;
const VARIANTS_RANGE = 10;

export default {
  data() {
    return {
      question: 'Oops, something went wrong...',
      correctAnswer: 0,
      variants: [
        { isCorrect: false, value: 0 },
        { isCorrect: false, value: 0 },
        { isCorrect: false, value: 0 },
        { isCorrect: false, value: 0 },
      ],
    };
  },
  methods: {
    generateRandomNumber(min, max, exclude) {
      const generated = Math.round(min + Math.random() * (max - min));
      if (exclude && generated === exclude) {
        return this.generateRandomNumber(min, max, exclude);
      }
      return generated;
    },
    generateQuestion() {
      const firstNumber = this.generateRandomNumber(1, 100);
      const secondNumber = this.generateRandomNumber(1, 100);
      const operation = this.generateRandomNumber(MATH_ADD, MATH_EXCLUDE);

      switch (operation) {
        case (MATH_ADD):
          this.question = `${firstNumber} + ${secondNumber} = ?`;
          this.correctAnswer = firstNumber + secondNumber;
          break;
        case (MATH_EXCLUDE):
          this.question = `${firstNumber} - ${secondNumber} = ?`;
          this.correctAnswer = firstNumber - secondNumber;
          break;
        default:
          this.question = 'Oops... something went wrong';
      }

      this.variants.forEach((variant, i) => {
        this.variants[i].value = this.generateRandomNumber(
          this.correctAnswer - VARIANTS_RANGE,
          this.correctAnswer + VARIANTS_RANGE,
          this.correctAnswer,
        );
      });

      const correctVariant = this.generateRandomNumber(0, this.variants.length);

      this.variants[correctVariant] = {
        isCorrect: true, value: this.correctAnswer,
      };
    },
  },
  created() {
    this.generateQuestion();
  },
};
</script>

<style scoped lang="scss">
ul {
  display: grid;
  grid-template-columns: 40% 40%;
  grid-row-gap: 2rem;
  grid-column-gap: 20%;
  margin: 0;
  padding: 0;
  list-style: none;
}

li {
  width: 50%;
  margin: 0 auto;
}

.variant {
  display: block;
  width: 100%;
  min-width: 22px;
  min-height: 22px;
}
</style>
