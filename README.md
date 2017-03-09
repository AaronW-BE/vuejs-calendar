[![Known Vulnerabilities](https://snyk.io/test/npm/vuejs-calendar/badge.svg)](https://snyk.io/test/npm/vuejs-calendar)

# vuejs-calendar
A calendar component for vuejs2

![screenshot](https://github.com/AaronWB/vuejs-calendar/raw/master/screenShot.png)

## Usage

## Install
` npm install vuejs-calendar --save `

## Reference in your project
> demo.vue
``` html
<template>
  <div>
    <calendar></calendar>
  </div>
</template>
import calendar from './components/Calendar.vue'
export default {
  name: 'app',
  components: {
      calendar
  },
...
}
```

## Optional Events
* ` dateChanged(date) `
* ` SwitchPreviousMonth(from, to) `
* ` SwitchNextMonth(from, to) `

## Props
* ` debug (default: false) `

## Example
```javascript
<template>
  <div>
    <calendar
      v-on:dateChanged="changed"
      v-on:SwitchPreviousMonth="pre"
      v-on:SwitchNextMonth="next"
      v-bind:debug="false"
    />
  </div>
</template>
```
```javascript
<script>
import calendar from 'vuejs-calendar'
export default {
  components: {
    calendar
  },
  methods: {
    pre (from, to){
      console.group('pre month')
        console.log('from',from)
        console.log('to',to)
      console.groupEnd()
    },
    next (from, to) {
      console.group('next month')
        console.log('from',from)
        console.log('to',to)
      console.groupEnd()
    },
    changed (to){
        console.log('changed to',to)
    }
  }
}
</script>
````

## Next Version
* Add custom active date
* support more style

# vuejs-calendar
一款vuejs日历组件

![screenshot](https://github.com/AaronWB/vuejs-calendar/raw/master/screenShot.png)

## 使用方法

## 安装
`npm install vuejs-calendar --save`
或
` cnpm install vuejs-calendar --save ` (淘宝npm镜像)

## 在项目中引用
> demo.vue
``` html
<template>
  <div>
    <calendar></calendar>
  </div>
</template>

import calendar from './components/Calendar.vue'
export default {
  name: 'app',
  components: {
      calendar
  },
...
}
```

## 可用事件
* ` dateChanged(date) ` 日期改变时触发
* ` SwitchPreviousMonth(from, to) ` 切换到上月时触发
* ` SwitchNextMonth(from, to) ` 切换到下月时触发

## props
* ` debug (default: false) `

## 示例
```html
<template>
  <div>
    <calendar
      v-on:dateChanged="changed"
      v-on:SwitchPreviousMonth="pre"
      v-on:SwitchNextMonth="next"
      v-bind:debug="false"
    />
  </div>
</template>
```
```javascript
<script>
import calendar from 'vuejs-calendar'
export default {
  components: {
    calendar
  },
  methods: {
    pre (from, to){
      console.group('pre month')
        console.log('from',from)
        console.log('to',to)
      console.groupEnd()
    },
    next (from, to) {
      console.group('next month')
        console.log('from',from)
        console.log('to',to)
      console.groupEnd()
    },
    changed (to){
        console.log('changed to',to)
    }
  }
}
</script>
````

# 下一个版本
* 增加自定义初始日期
* 增加更多样式

## ` Features`
* 农历支持