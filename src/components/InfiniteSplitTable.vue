<template>
  <table
    class="infinite-split-table"
    cellpadding="0"
    cellspacing="0"
    :class="{'top-border':deep==0,'left-border':deep==0}">
    <template v-if="tree_data.type=='column'">
      <!--纵向排列-->
      <tr
        v-for="(item,index) in tree_data.data"
        style="width: 100%;"
        :style="{height:typeof item.height!='undefined'?item.height:'auto'}">
        <td>
          <infinite-split-table-item
          :tree_data="tree_data"
          :item="item"
          :index="index"
          :deep="deep">
          </infinite-split-table-item>
        </td>
      </tr>
    </template>
    <template v-else-if="tree_data.type=='row'">
      <!--横向排列-->
      <tr>
        <td
          v-for="(item,index) in tree_data.data"
          :style="{width:typeof item.width!='undefined'?item.width:'auto'}">
          <infinite-split-table-item
          :tree_data="tree_data"
          :item="item"
          :index="index"
          :deep="deep">
          </infinite-split-table-item>
        </td>
      </tr>
    </template>
  </table>
</template>
<script>
  export default{
    name:'InfiniteSplitTable',
    components:{
      InfiniteSplitTableItem:()=>import('./InfiniteSplitTableItem.vue')
    },
    props:['tree_data','deep'],
  }
</script>
<style scoped>
  .infinite-split-table{
    width: 100%;height: 100%;box-sizing: border-box;
  }
  .left-border{
    border-left: 1px solid black;
  }
  .top-border{
    border-top: 1px solid black;
  }
</style>
