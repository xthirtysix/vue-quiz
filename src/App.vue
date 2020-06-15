<template>
  <div id="app" class="container">
    <h1>{{ header }}</h1>
    <hr>
    <app-question/>
  </div>
</template>

<script>
import Question from './components/Question.vue';

export default {
  name: 'quizz-app',
  data() {
    return {
      header: 'Quiz app',
    };
  },
  components: {
    appQuestion: Question,
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
