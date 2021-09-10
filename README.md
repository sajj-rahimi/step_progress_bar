# vue-step-progress-bar

## Install the plugin with npm:

```
npm install vue-step-progress-bar
```

## Usage

import the component and pass the options

```javascipt
<template>
    <step-progress-bar :options="options" ref="progress" />
</tepmlate>

<script>
import StepProgressBar from 'vue-step-progress-bar'

export default {
  data () {
    return {
      options: {
          maxWidth:'100%',
          nodeWidth:40,
          nodeHeight:40,
          barHeight:3,
          showTooltip:true,
          showContent:true,

          #barType can be dashed or solid
          barType:'dashed',

          #expects a function
          onNext:this.onNext,

          #expects a function
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
  }
}
</script>
```

call component methods using ref

```javascript
methods: {
    someDummyFunction() {
        #goes to the next step
        this.$refs.progress.next()

        #goes to the previous step
        this.$refs.progress.prev()

        #restarts the step progress bar
        this.$refs.progress.restart()
    }
}
```

### That's it :)

![alt text](https://github.com/sajj-rahimi/step_progress_bar/tree/develop/step-progress-bar.png?raw=true)
