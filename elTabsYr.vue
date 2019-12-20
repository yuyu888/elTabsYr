<template>
    <el-row >
      <template v-for="tab in tabs">
      <el-button v-if="tab.value==currentTabVal && tab.key==currentTabKey" :key="tab.index" :size="size" :type="type" v-on:click="tabClickHandler(tab.key, tab.value)" plain >{{tab.name}}</el-button>
      <el-button v-else :key="tab.index" :size="size" v-on:click="tabClickHandler(tab.key, tab.value)" plain  >{{tab.name}}</el-button>
      </template>
    </el-row>
 </template>
<script>

export default {
  name: 'elTabsYr',
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
  data() {
    return {
      currentTabKey: this.currentKey,
      currentTabVal: this.currentVal
    }
  },
  watch: {
    currentKey(newVal, oldVal) {
      this.currentTabKey = newVal
    },
    currentVal(newVal, oldVal) {
      this.currentTabVal = newVal
    }
  },
  created() {
    this.initData()
  },
  methods: {
    initData() {
    },
    tabClickHandler(key, val) {
      if (this.currentTabKey === key && this.currentTabVal === val) {
        this.currentTabKey = key = ''
        this.currentTabVal = val = ''
      } else {
        this.currentTabKey = key
        this.currentTabVal = val
      }
      this.$emit('changeTab', key, val)
    }
  }
}
</script>
