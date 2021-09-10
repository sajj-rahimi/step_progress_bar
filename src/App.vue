<template>
<div class="main-container">
  <step-progress-bar :options="options" ref="progress" />
  <div class="operations">
        <div class="button-container">
          <button class="next" @click="next()">next</button>
          <button class="prev" @click="prev()">prev</button>
          <button class="restart" @click="restart()">restart</button>
        </div>
        <div class="input-container">
          <div class="input-group">
            <label for="barHeight-input">bar height :</label>
            <input type="number" v-model="options.barHeight" name="" id="barHeight-input">
          </div>
          <div class="input-group">
            <label for="node-width-input">node width :</label>
            <input type="number" v-model="options.nodeWidth" name="" id="node-width-input">
          </div>
          <div class="input-group">
            <label for="nodeHeight-input">node height :</label>
            <input type="number" v-model="options.nodeHeight" name="" id="nodeHeight-input">
          </div>
        </div>
  </div>
</div>
  
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
                content:'salam salam salamsalam salam salam ',
                tooltip:'salam slam salam salam salam salam salam salam'
              },
              {
                content:'salam',
                tooltip:'chetori?'
              },
              {
                content:'salam',
                tooltip:'chetori?'
              },
              {
                content:'salam',
                tooltip:'chetori?'
              },
              {
                content:'salam',
                tooltip:'chetori?'
              },
              {
                content:'salam',
                tooltip:'chetori?'
              }
            ]
      }
    }
  },
  created(){
    // setTimeout(() => {
    //    this.$refs.progress.next()
    // }, 20);
   
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
