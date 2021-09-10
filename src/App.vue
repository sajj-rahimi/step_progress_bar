<template>
  <step-progress-bar :options="options" ref="progress" />
</template>

<script>
import StepProgressBar from './components/StepProgressBar.vue'

export default {
  name: 'App',
  components: {
    StepProgressBar
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
