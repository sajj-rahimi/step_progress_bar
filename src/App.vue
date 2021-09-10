<template>
  <step-progress-bar :options="options" ref="progress" />
</template>

<script>
import StepProgressBar from './components/StepProgressBar.vue'

export default {
  name: 'App',
  components: {
    StepProgressBar
  },
  data(){
    return{
      options:{
          maxWidth:'100%',
          nodeWidth:40,
          nodeHeight:40,
          barHeight:3,
          showTooltip:true,
          showContent:true,
          barType:'dashed',
          onNext:this.onNext,
          onFinish:this.onFinish,
          nodes:[
              {
                content:'step 1',
                tooltip:'sth about step 1'
              },
              {
                content:'step 2',
                tooltip:'sth about step 2'
              },
              {
                content:'step 3',
                tooltip:'sth about step 3'
              },
              {
                content:'step 4',
                tooltip:'sth about step 4'
              }
            ]
      }
    }
  },
  methods:{
    onNext(){
      console.log('onNext')
    },
    onFinish(){
      console.log('finshed')
    },
    next(){
      this.$refs.progress.next()
    },
    prev(){
      this.$refs.progress.prev()
    },
    restart(){
      this.$refs.progress.restart()
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
