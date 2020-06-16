<template>
  <div id="app" class="container">
    <h1>{{ header }}</h1>
    <hr>
    <transition>
      <component
        :is="mode"
        @confirmed="mode = 'app-question'"
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
</style>
