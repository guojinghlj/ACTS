<template>
  <div class="home">
    <textarea name="" v-model="input" id="" cols="30" rows="10"></textarea>
    <button @click="render">开始</button>
    {{msg}}
    <Tree :data="json"></Tree>
    <button @click="print">打印</button>
  </div>
</template>

<script>
// @ is an alias to /src
import Tree from '@/components/Tree.vue'

export default {
  name: 'home',
  data() {
    return {
      input: `{
    "list": [
        {
            "name": "黄焖鸡米饭111111111",
            "cList": [
                {
                    "name": "二级黄焖鸡"
                },
                {
                    "name": "one chicken",
                    "cList": [
                        {
                            "name": "三级黄焖鸡3333",
                            "cList": [
                                {
                                    "name": "四级黄焖鸡"
                                }
                            ]
                        }
                    ]
                }
            ]
        },
        {
            "name": "2222222222"
        },
        {
            "name": "黄焖鸡米饭33333333",
            "cList": [
                {
                    "name": "二级黄焖鸡"
                },
                {
                    "name": "one chicken"
                }
            ]
        }
    ],
    "ct": 12123123123,
    "test": "234234"
}`,
      json: {},
      msg: ''
    }
  },
  components: {
    Tree
  },
  methods: {
    onBlur() {

      this.render()
    },
    render() {
      this.format()
    },
    format() {
      try {
        this.json = JSON.parse(this.input)
        this.msg = ''
      } catch(err) {
        this.msg = 'json 格式错误'
      }
    },
    print() {
      console.log(JSON.stringify(this.json))
    }
  }
}
</script>
<style lang="less">
  .home {
    display: flex;
    flex-direction: column;
  }
</style>