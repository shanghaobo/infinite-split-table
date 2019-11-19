<template>
  <table
    class="infinite-split-table"
    cellpadding="0"
    cellspacing="0"
    :class="{'top-border':deep==0,'left-border':deep==0}">
    <template>
      <tr
        v-for="line in for_data"
        style="width: 100%;"
        :style="{height:typeof line[0].height!='undefined'?line[0].height:'auto'}">
        <td
          v-for="item in line"
          :style="{width:typeof item.width!='undefined'?item.width:'auto'}">
          <div v-if="item.type!='row'&&item.type!='column'" class="text">
            <span v-if="item.type=='label'">
              {{item.data}}
            </span>
          </div>
          <!--递归调用-->
          <infinite-split-table
            v-else
            :tree_data="item"
            :deep="deep+1">
          </infinite-split-table>
        </td>
      </tr>
    </template>
  </table>
</template>
<script>
  export default{
    name:'InfiniteSplitTable',
    props:['tree_data','deep'],
    computed:{
      for_data(){
        let type=this.tree_data.type;
        let data=this.tree_data.data;
        let result=[];
        if(type==='row'){
          result.push(data);
        }
        else if(type==='column'){
          for(let i=0;i<data.length;i++){
            result.push([data[i]]);
          }
        }
        return result;
      }
    }
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
