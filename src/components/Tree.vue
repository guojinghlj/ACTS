<template>
<div :class="['tree', !isObjectOrArray && 'inline']">
  
  <div class="dom-node" v-if="isObjectOrArray">
    <span>{</span>
    <button v-if="isExpend" class="btn ml-20" @click="doExpend(false)">-</button>
    <button v-else class="btn ml-20" @click="doExpend(true)">+</button>

    <div class="children" v-if="isExpend">
      <div class="node ml-20" v-for="(key,index) in parents" :key="index">
        "{{key}}": 
        <Tree :data="getChildren(key)"></Tree>
      </div>
    </div>
    <div v-else class="empty">
      <div @click="doExpend(true)">{{len}} ...</div>
    </div>
    <span>}</span>
  </div>
  <div v-else-if="!isObjectOrArray" class="node-text">
    {{data}}
  </div>
</div>  
</template>
<script>
export default {
  name: 'Tree',
  data() {
    return {
      isExpend: true
    }
  },
  computed: {
    len() {
      return this.parents.length
    },
    parents() {
      if(this.isObjectOrArray && this.data) {
        return Object.keys(this.data)
      }
      return []
    },
    isObjectOrArray() {
      return typeof this.data === 'object' || this.data instanceof Array
    }
  },
  props: {
    data: {
      type: Object|Array,
      default() {
        return {}
      }
    },
    
  },
  methods: {
      doExpend(ex) {
        this.isExpend = ex
      },
      getChildren(key) {
        return this.data[key] || null
      }
    },
}
</script>
<style lang="less">
  .ml-20 {
    margin-left: 20px;
  }
  .btn {
    width: 20px;
    height: 20px;
    display: inline-block;
  }
  .tree {
    display: flex;
    &.inline {
      display: inline;
    }
    .children {
      .node {
        margin-left: 20px;
      }
    }
  }
  .node-text {
    display: inline;
  }
</style>