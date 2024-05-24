1. 编写组件

```vue
<!-- AntIcon.vue -->

<template>
  <component :is="icons[iconName]" v-bind="$attrs"></component>
</template>

<script setup>
import { computed } from 'vue'
import * as icons from '@ant-design/icons-vue'

const props = defineProps({
  // icon图标名称
  type: {
    type: String,
    default: 'FireOutlined'
  }
})

/** 转化icon名称 */
const iconName = computed(() => {
  if (!props.type.includes('-')) {
    return props.type
  }
  return (
    props.type.charAt(0).toUpperCase() +
    props.type.slice(1).replace(/-([a-z])/g, function (g) {
      return g[1].toUpperCase()
    })
  )
})
</script>
```

2. 注册组件

```js
import AntIcon from '@/components/AntIcon.vue'

const app = createApp(App)
app.component('ant-icon', AntIcon)
app.mount('#app')
```

3. 使用

```vue
<ant-icon type="HomeOutlined"></ant-icon>
```

