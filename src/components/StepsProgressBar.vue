<template>
    <div class="progress-container" :style="{maxWidth:options.maxWidth}">
      <div class="progress" v-for="(node, index) in options.nodes" :id="index" :key="index">
        <div  class="node" 
        :style="{width:options.nodeWidth+'px', height:options.nodeHeight + 'px'}"
        :class="[`node-${index}`,{'start-node active': index===0} , {'last-node': index+1===options.nodes.length}]" :id="index">
          <div class="node-circle" :id="index">{{index+1}}</div>
          <div v-if="options.showContent" class="node-content"><p>{{node.content}}</p></div>
          <div v-if="options.showTooltip" class="tooltip-container">
            <div class="node-tooltip" 
              :class="[`node-tooltip-${index}`, index%2===0 ? 'node-tooltip-top' : 'node-tooltip-down']">
                <p class="tooltip-text" style="position:relative"> {{node.tooltip}}</p>
            </div>
          </div>
        </div>
        <div class="progress-bar"  :class="[`bar-${index}`]" v-if="(index + 1)!==(options.nodes.length)" :id="index">
          <div class="progress-bar-active" :style="{borderTop:options.barHeight + `px ${options.barType} #bbbbbb`}">
          </div>
          <div class="progress-bar-checked" :style="{borderTop:options.barHeight + 'px solid #61B15A'}"></div>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'StepsProgressBar',
  props:{
    options:{
      type:Object, default:function(){
          return {
          maxWidth:'100%',
          nodeWidth:40,
          nodeHeight:40,
          barHeight:3,
          showTooltip:true,
          showContent:true,
          barType:'dashed',
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
     }
  },
  created(){
    setTimeout(this.handleHover , 20)
  },
  methods:{
   next(){
      if(this.options?.beforeNext){
        this.options.onNext()
      }
      let currNode = document.querySelector('.node.active')
      if(currNode){
        let currNodeIndex = Number(currNode.getAttribute('id'))

        currNode.classList.remove('active')
        currNode.classList.add('checked')
        currNode.firstElementChild.innerHTML=''

        if(currNodeIndex!==this.options.nodes.length-1){
          let nextNode = document.querySelector(`.node.node-${currNodeIndex+1}`)
          nextNode.classList.add('active')

          let currBar = document.querySelector(`.bar-${currNodeIndex}`)
          currBar.classList.add('checked')
        } else if (this.options?.onFinish) {
          this.options.onFinish()
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
          currNode.firstElementChild.innerHTML=currNodeIndex+1

          let prevNode = document.querySelector(`.node.node-${currNodeIndex-1}`)
          prevNode.classList.remove('checked')
          prevNode.firstElementChild.innerHTML=''
          prevNode.firstElementChild.innerHTML=currNodeIndex
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
     if(this.options.showTooltip){
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
}
</script>

