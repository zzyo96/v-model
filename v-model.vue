<template>
  <div>
    <a-tree-select
      :dropdownStyle="{ maxHeight: '200px', overflow: 'auto' }"
      :loadData="loadData"
      :multiple="multiple"
      :treeCheckable="multiple"
      :treeData="treeData"
      @change="onChange"
      @search="onSearch"
      @select="onSelect"
      allowClear
      placeholder="请选择..."
      showSearch
      style="width: 300px"
      treeDefaultExpandAll
      treeNodeFilterProp="title"
      v-model="selected"
    />
    <!--treeDefaultExpandAll-->
  </div>
</template>

<script>
  import {getAction} from '@/api/manage'

  export default {
    name: "TreeSelectUser",
    model: {
      prop: "value",
      event: 'change'
    },
    props: {
      value: {
        type: [String, Array],
        require: true
      },
      lazyLoad: {
        type: Boolean,
        default: false
      },
      multiple: {
        type: Boolean,
        require: false
      }
    },
    computed: {
      selected: {
        get() {
          return this.value
        },
        set(value) {
          this.$emit("change", value)
        }
      }
    },
    data() {
      return {
        treeData: []
      }
    },
    methods: {
      loadData(treeNode) {
       
      },
      loadRoot() {
        
      },
      //同步加载数据
      onloadData() {
    
      },
      onChange(value, label) {
        this.$emit("change", value, label)
      },
      onSearch() {
        this.$emit("search", ...arguments)
        // console.log(...arguments);
      },
      onSelect() {
        this.$emit("select", ...arguments)
        // console.log(...arguments);
      }
    },
    created() {
      if (this.lazyLoad) {
        this.loadRoot()
      } else {
        this.onloadData()
      }
    }
  }
</script>
