<template>
  <div class="main-container">
    <div class="progress-container">
      <div class="progress" v-for="(node, index) in nodes" :id="index" :key="index">
        <div  class="node" 
        :style="{width:nodeWidth+'px', height:nodeHeight + 'px'}"
        :class="[`node-${index}`,{'start-node active': index===0} , {'last-node': index+1===nodes.length}]" :id="index">
          <div class="node-circle" :id="index">{{index}}</div>
          <div class="node-content"><p>{{node.content}}</p></div>
          <div v-if="showTooltip" class="tooltip-container">
            <div class="node-tooltip" 
              :class="[`node-tooltip-${index}`, index%2===0 ? 'node-tooltip-top' : 'node-tooltip-down']">
                <p class="tooltip-text" style="position:relative"> {{node.tooltip}}</p>
            </div>
          </div>
        </div>
        <div class="progress-bar"  :class="[`bar-${index}`]" v-if="(index + 1)!==(nodes.length)" :id="index">
          <div class="progress-bar-active" :style="{borderTop:barHeight + 'px dashed #bbbbbb'}">
          </div>
          <div class="progress-bar-checked" :style="{borderTop:barHeight + 'px solid #61b15a'}"></div>
        </div>
      </div>
    </div>
      <div class="operations">
        <div class="button-container">
          <button class="next" @click="next()">next</button>
          <button class="prev" @click="prev()">prev</button>
          <button class="restart" @click="restart()">restart</button>
        </div>
        <div class="input-container">
          <div class="input-group">
            <label for="barHeight-input">bar height :</label>
            <input type="number" v-model="barHeight" name="" id="barHeight-input">
          </div>
          <div class="input-group">
            <label for="node-width-input">node width :</label>
            <input type="number" v-model="nodeWidth" name="" id="node-width-input">
          </div>
          <div class="input-group">
            <label for="nodeHeight-input">node height :</label>
            <input type="number" v-model="nodeHeight" name="" id="nodeHeight-input">
          </div>
        </div>
      </div>
  </div>
</template>

<script>
import '@/assets/index.scss'
export default {
  name: 'HelloWorld',
  data(){
    return{
      nodeWidth:40,
      nodeHeight:40,
      barHeight:3,
      showTooltip:true,
       nodes:[
          {
            content:'salam',
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
  },
  created(){
    setTimeout(this.handleHover , 20)
  },
  methods:{
   next(){
      let currNode = document.querySelector('.node.active')
      if(currNode){
        let currNodeIndex = Number(currNode.getAttribute('id'))

        currNode.classList.remove('active')
        currNode.classList.add('checked')
        currNode.firstElementChild.innerHTML=''

        if(currNodeIndex!==this.nodes.length-1){
          let nextNode = document.querySelector(`.node.node-${currNodeIndex+1}`)
          nextNode.classList.add('active')

          let currBar = document.querySelector(`.bar-${currNodeIndex}`)
          currBar.classList.add('checked')
        }
      } 
   },
   prev(){
      let currNode = document.querySelector('.node.active') ? document.querySelector('.node.active') : document.querySelector('.last-node')
      if(currNode){
        let currNodeIndex = Number(currNode.getAttribute('id'))

        if(currNodeIndex!==0){
          currNode.classList.remove('active')
          currNode.classList.remove('checked')
          currNode.firstElementChild.innerHTML=''
          currNode.firstElementChild.innerHTML=currNodeIndex

          let prevNode = document.querySelector(`.node.node-${currNodeIndex-1}`)
          prevNode.classList.remove('checked')
          prevNode.firstElementChild.innerHTML=''
          prevNode.firstElementChild.innerHTML=currNodeIndex-1
          prevNode.classList.add('active')

          let prevBar = document.querySelector(`.bar-${currNodeIndex-1}`)
          prevBar.classList.remove('checked')
        }
      } 
   },
   restart(){
      document.querySelectorAll('.node').forEach((node , index)  => {
          node.classList.remove('checked')
          node.classList.remove('active')
          node.firstElementChild.innerHTML = index
          if(node.classList.contains('start-node')){
            node.classList.add('active')
          }
      })
      document.querySelectorAll('.progress-bar').forEach(bar=>{
        bar.classList.remove('checked')
      })
   },
   handleHover(){
     document.querySelectorAll('.node-circle').forEach(node=>{
       const index = node.getAttribute('id')
       node.addEventListener('mouseover', function(){
         document.querySelectorAll('.node-tooltip').forEach(item=>{item.classList.remove('remove-tooltip'),item.classList.remove('show-tooltip')})
           document.querySelector(`.node-tooltip.node-tooltip-${index}`).classList.add('show-tooltip')
       })
       node.addEventListener('mouseleave', function(){
           document.querySelectorAll('.node-tooltip').forEach(item=>{item.classList.remove('remove-tooltip'),item.classList.remove('show-tooltip')})
           document.querySelector(`.node-tooltip.node-tooltip-${index}`).classList.add('remove-tooltip')
       })
     })
   }
 }
}
</script>

