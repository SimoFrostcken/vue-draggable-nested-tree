<!-- this is an example -->
<template lang="pug">
div(dir="rtl")
  h2 RTL
  Tree(:data="originalData" draggable crossTree ref="tree1" @drag="ondrag")
    div(slot-scope="{data, store}")
      b(v-if="data.children && data.children.length" @click="store.toggleOpen(data)") {{data.open ? '-' : '+'}}&nbsp;
      span {{data.text}}-droppable:{{data.droppable}}
</template>

<script>
import Tree from '@/components/DraggableTree'
import * as th from 'tree-helper'

export default {
  components: {Tree},
  data() {
    return {
      originalData: [
        {text: 'node 1'},
        {text: 'node 2'},
        {text: 'node 3'},
        {text: 'node 4'},
        {text: 'node 4 undroppable', droppable: false},
        {text: 'node 5', children: [
          {text: 'node 1'},
          {text: 'node 2', children: [
            {text: 'node 3'},
            {text: 'node 4'},
          ]},
          {text: 'node 2 undroppable', droppable: false, children: [
            {text: 'node 3'},
            {text: 'node 4'},
          ]},
          {text: 'node 2', children: [
            {text: 'node 3'},
            {text: 'node 4 undroppable', droppable: false},
          ]},
          {text: 'node 3'},
          {text: 'node 4'},
          {text: 'node 3'},
          {text: 'node 4'},
          {text: 'node 3'},
          {text: 'node 4'},
          {text: 'node 3'},
          {text: 'node 4'},
        ]},
      ],
      data: null,
    }
  },
  // computed: {},
  // watch: {},
  methods: {
    ondrag(node, targetTree) {
      this.data = targetTree.getPureData()
    },
  },
  // created() {},
  // mounted() {},
}
</script>

<style>
</style>
