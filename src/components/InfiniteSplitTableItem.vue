<template>
  <div style="width: 100%;height: 100%">
    <div
      v-if="item.type!='row'&&item.type!='column'"
      class="text">
      <span v-if="item.type=='label'">
        {{item.data}}
      </span>
    </div>
    <infinite-split-table
      v-else
      :tree_data="item"
      :deep="deep+1">
    </infinite-split-table>
  </div>
</template>
<script>
  export default{
    name:'InfiniteSplitTableItem',
    components:{
      InfiniteSplitTable:()=>import('./InfiniteSplitTable.vue')
    },
    props:['tree_data','item','index','deep'],
  }
</script>
<style scoped>
  .text{
    padding: 5px;
    box-sizing: border-box;
    border-right: 1px solid black;
    border-bottom: 1px solid black;
    height: 100%;
    min-height: 30px;
    word-wrap: break-word;
    word-break: break-all;
  }
</style>
