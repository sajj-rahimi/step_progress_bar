<template>
  <div class="main-container">
    <div class="progress-container">
      <div class="progress" v-for="(node, index) in nodes" :id="index" :key="index">
        <div  class="node" :class="[`node-${index}`,{'start-node active': index===0} , {'last-node': index+1===nodes.length}]" :id="index">
          <div class="node-circle">{{index}}</div>
          <div class="node-content">{{node.content}}</div>
          <div class="node-tooltip" 
            :style="[{top: index%2===0 ? '-150%' : '200%'},
                    {transform:index%2===0 ? 'translateY(30px) translateX(-50%)' : 'translateY(-30px) translateX(-50%)'}
                    ]">
              {{node.tooltip}}
          </div>
        </div>
        <div class="progress-bar" :class="[`bar-${index}`]" v-if="(index + 1)!==(nodes.length)" :id="index"></div>
      </div>
    </div>
      <div class="operations">
        <button class="next" @click="next()">next</button>
        <button class="prev" @click="prev()">prev</button>
        <button class="restart" @click="restart()">restart</button>
      </div>
  </div>
</template>

<script>
import '@/assets/index.scss'
export default {
  name: 'HelloWorld',
  data(){
    return{
       nodes:[
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
          },
          {
            content:'salam',
            tooltip:'chetori?'
          }
        ]
    }
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
   }
 }
}
</script>

