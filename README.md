# event
简单实现组件通信

# 自定义流程图

## 安装

推荐使用 npm 的方式安装，它能更好地和 webpack 打包工具配合使用

`npm i name -S`

## 快速上手

```vue
<template>
  <div id="app">
    <FlowChart height="800px" ref="flowChart" @node:selected="nodeChange">
      <template v-slot:sideBar>
        <div class="rightMsg">
          <div class="title">查看编辑</div>
          <input
            type="text"
            v-model="selectedNodes.label"
            placeholder="请输入标题"
          >
          <textarea
            placeholder="请输入描述信息"
            v-model="selectedNodes.description"
            cols="30"
            rows="3"
          >
          </textarea>
          <Button @click="handlerClick">保存</Button>
        </div>
      </template>
    </FlowChart>
  </div>
</template>

<script>
import FlowChart from 'name'

export default {
  name: 'App',
  components: {
    FlowChart
  },
  data () {
    return {
      selectedNodes: {}
    }
  },
  methods: {
    handlerClick () {
      if (this.selectedNodes) {
        this.$refs.flowChart.updateItem(this.selectedNodes)
        this.$refs.flowChart.toggleSidebar()
      }
    },
    nodeChange (nodes) {
      this.selectedNodes = nodes
    }
  }
}
</script>
```

## API

### FlowChart Attributes

| 参数            | 说明                                                              | 类型   | 默认值 |
| --------------- | ---------------------------------------------------------------- | ------ | ------ |
| width           | 指定画布宽度，单位为 'px'                                           | number | 1200     |
| height          | 指定画布高度，单位为 'px'                                           | number  | 600  |
| data            | 显示的图表数据 [配置项](#data)                                      | object | {nodes: [], edges: []}     |
| statusColor     | 节点状态颜色 (success/error/normal)                            | object | {success: { color:        '#67C23A' }, error: { color: '#F56C6C' }, normal: { color: '#409EFF' }}     |


#### data

```js
data: {
    nodes: [
        {
            id: 'xxx1',
            label: '我是 title',
            state: '我是节点状态',
            description: '我是节点描述',
            task: {} // 根据项目需求自定义
        },
        {
            id: 'xxx2',
            label: '我是 title',
            state: '我是节点状态',
            description: '我是节点描述',
            task: {} // 根据项目需求自定义
        }
    ],
    edges: [
        {
            source: 'xxx1',
            target: 'xxx2',
        }
    ]
}
```

### FlowChart Events

| 事件名           | 说明                                                              | 参数   |
| --------------- | ---------------------------------------------------------------- | ------ |
| node-selected   | 当用户手动点击当前节点查看按钮触发的事件                                | node |

### FlowChart Methods

| 方法名           | 说明                                          | 参数   |
| --------------- | -------------------------------------------- | ------ |
| updateItem      | 用于更新节点数据                                | node |
| toggleSidebar   | 用于切换抽屉的状态                              | - |
| getData         | 用于用户获取当前数据                            | - |


### FlowChart Slot

| slot name       | 说明                                          |
| --------------- | -------------------------------------------- |
| sideBar         | 抽屉的内容，如果需要编辑当前节点，需要自定义 dom ，并且提交数据的时候调用 updateItem 方法更新节点信息｜
