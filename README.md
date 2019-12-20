## 概要
该组件使用vue 基于element-ui编写，提供了一种tabs切换样式，并且配置灵活 可自行配置灵活组合使用

## 引用范例
  ```javascript
    <el-tabs-yr v-if="statusTabs"
      :tabs="statusTabs" 
      key="status" 
      currentKey="status" 
      :currentVal="currentStatusTabVal"
      size="mini" 
      type="primary" 
      v-on:changeTab="changeStatus">
    </el-tabs-yr>
    
  ```
## prop说明

  ```javascript
    props: {
        tabs: {
            type: Array,
            required: true
        },
        size: {
            type: String,
            default: 'mini'
        },
        type: {
            type: String,
            default: 'primary'
        },
        currentVal: {
            type: String,
            default: ''
        },
        currentKey: {
            type: String,
            default: ''
        }
    },
  ```

#### tabs
  tabs数据,要求是一个数组

  1. key: 变量定义
  2. name: 变量描述（名称）
  3. value: 变量值
  
  key 可以根据需要，不要求一致
  
  示例
  ```javascript
  statusTabs: [
          {
            key: 'status',
            name: '全部',
            value: '0'
          },
          {
            key: 'status',
            name: '待处理',
            value: '1'
          },
          {
            key: 'status',
            name: '跟进中',
            value: '2'
          },
          {
            key: 'status',
            name: '已完结',
            value: '3'
          }
        ],
  ```

#### key
  非必要，同时还有多个组件时，可以设置不同的值做标示

#### size
  尺寸
  
  可选值
  medium / small / mini


#### type
  类型 / 颜色控制
  
  可选值 primary / success / warning / danger / info / text


#### currentKey
  当前选中key
  
#### currentVal
   当前选中值

#### changeTab
  tab切换时回调方法
  
  示例
   ```javascript

  changeStatus(key, val) {
    console.log(key, val)
  }
  ```
  
## 高级用法
  两个tabs 同时存在并联动

  ```javascript
  
  <template>
      <div>
          <el-tabs-yr v-if="statusTabs"
            :tabs="statusTabs" 
            key="status" 
            currentKey="status" 
            :currentVal="currentStatusTabVal"
            size="mini" 
            type="primary" 
            v-on:changeTab="changeStatus">
          </el-tabs-yr>
          <br/>        <br/>
  
          <el-tabs-yr v-if="customTabs && currentStatusTabVal==='2'"
            :tabs="customTabs" 
            key="custom" 
            :currentKey="currentCustomTabKey" 
            :currentVal="currentCustomTabVal"
            size="mini" 
            type="primary" 
            v-on:changeTab="changeCustomTab">
          </el-tabs-yr>
      </div>
  </template>
  <script>
  import ElTabsYr from '@/components/elTabsYr.vue'
  
  export default {
    name: 'Test',
    components: {
      ElTabsYr
    },
    data() {
      return {
        statusTabs: [
          {
            key: 'status',
            name: '全部',
            value: '0'
          },
          {
            key: 'status',
            name: '待处理',
            value: '1'
          },
          {
            key: 'status',
            name: '跟进中',
            value: '2'
          },
          {
            key: 'status',
            name: '已完结',
            value: '3'
          }
        ],
        currentStatusTabVal: '1',
        customTabs: [
          {
            key: 'selectAll',
            name: '全部',
            value: '1'
          },
          {
            key: 'is_shelved',
            name: '待回复',
            value: '1'
          },
          {
            key: 'reparation_status',
            name: '需赔付',
            value: '1'
          },
          {
            key: 'reparation_status',
            name: '赔付中',
            value: '2'
          },
          {
            key: 'reparation_status',
            name: '赔付完成',
            value: '3'
          }
        ],
        currentCustomTabKey: 'selectAll',
        currentCustomTabVal: '1'
      }
    },
    created() {
    },
    methods: {
      changeStatus(key, val) {
        console.log(key, val)
        this.currentStatusTabVal = val
        if (val === '2') {
          this.currentCustomTabKey = 'selectAll'
          this.currentCustomTabVal = '1'
        }
        // this.currentPage = 1
        // this.getList()
      },
      changeCustomTab(key, val) {
        this.currentCustomTabKey = key
        this.currentCustomTabVal = val
        if (key === 'selectAll' && val === '1') {
          console.log(1111)
          // TODO
        }
        console.log(key, val)
      }
    }
  }
  </script>
  
  
  
  ```

