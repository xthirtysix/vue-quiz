<template>
  <div>
    <b-alert
      show
      style="max-width: 40rem; margin: 0 auto;"
      variant="success">
      <h4 class="alert-heading">Well done!</h4>
      <hr>
       <b-button variant="primary" @click="onNextQuestion">Next question</b-button>
    </b-alert>
  </div>
</template>

<script>
export default {
  methods: {
    onNextQuestion() {
      this.$emit('confirmed');
    },
  },
};
</script>

<style lang="scss" scoped>

</style>
