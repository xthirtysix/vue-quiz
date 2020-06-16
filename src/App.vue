<template>
  <div id="app" class="container">
    <h1>{{ header }}</h1>
    <hr>
    <p style="max-width: 40rem; margin: 0 auto 1rem; text-align: right">
      Correct answers: {{ correctCount }}
    </p>
    <transition name="flip" mode="out-in">
      <component
        :is="mode"
        :getHeight="getHeight"
        @confirmed="mode = 'app-question', height = 0"
        @answered="answered($event)"
      />
    </transition>
  </div>
</template>

<script>
import Question from './components/Question.vue';
import Answer from './components/Answer.vue';

export default {
  name: 'quizz-app',
  data() {
    return {
      header: 'Quiz app',
      mode: 'app-question',
      correctCount: 0,
    };
  },
  components: {
    appQuestion: Question,
    appAnswer: Answer,
  },
  methods: {
    answered(isCorrect) {
      if (isCorrect) {
        this.mode = 'app-answer';
        this.correctCount += 1;
      }
    },
  },
};
</script>

<style lang="scss">
@import "./scss/custom.scss";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.flip-enter-active {
  animation: flip-in 0.5s ease-out forwards;
}

.flip-leave-active {
  animation: flip-out 0.5s ease-out forwards;
}

@keyframes flip-out {
  from {
    transform: rotateY(0);
  } to {
    transform: rotateY(90deg);
  }
}

@keyframes flip-in {
  from {
    transform: rotateY(90deg);
  } to {
    transform: rotateY(0);
  }
}
</style>
