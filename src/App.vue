<template>
  <steps-progress-bar :options="options" ref="progress" />
</template>

<script>
import StepsProgressBar from './components/StepsProgressBar.vue'

export default {
  name: 'App',
  components: {
    StepsProgressBar
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
