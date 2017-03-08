[![Known Vulnerabilities](https://snyk.io/test/npm/vuejs-calendar/badge.svg)](https://snyk.io/test/npm/vuejs-calendar)

# vuejs-calendar
A calendar component for vuejs2

![screenshot](https://github.com/AaronWB/vuejs-calendar/raw/master/screenShot.png)

# Usage

## install
· npm install vuejs-calendar ·

## reference in your project
 demo.vue
```
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

# Optional Events
* dateChanged(date)
* SwitchPreviousMonth(from, to)
* SwitchNextMonth(from, to)


# vuejs-calendar
一款vuejs日历组件

![screenshot](https://github.com/AaronWB/vuejs-calendar/raw/master/screenShot.png)

# 使用方法

## 安装
·npm install vuejs-calendar·
或
·cnpm install vuejs-calendar· (淘宝npm镜像)

## 在项目中引用
> demo.vue
```
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

# 可用事件
* dateChanged(date) 日期改变时触发
* SwitchPreviousMonth(from, to) 切换到上月时触发
* SwitchNextMonth(from, to) 切换到下月时触发