<template>
  <h1>Cascader 示例</h1>
  <Demo :component="CascaderDemo2" />
  <Demo :component="CascaderDemo1" />
</template>
<script lang="ts">
import Demo from './Demo.vue';
import CascaderDemo2 from './Cascader2.demo.vue'
import CascaderDemo1 from './Cascader1.demo.vue'
import db from '../db.js'
import {ref} from 'vue';
import Cascader from '../lib/Cascader/Cascader.vue';

function ajax(parentId) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      let result = (db as Array<any>).filter(item => item.parent_id === parentId).map(item => {return {...item, label: item.name};});
      result.forEach(node=>{
        if((db as Array<any>).filter(item=>item.parent_id === node.id).length > 0){
          node.isLeaf = false
        }else{
          node.isLeaf = true
        }
      })
      resolve(result);
    }, 300);
  });
}


export default {
  components: {Demo,CascaderDemo2,CascaderDemo1,Cascader},
  setup(){
    const option = ref([]);
    const selected = ref([])
    const loadData = (node,callback) => {
      let {id} = node;
      ajax(id).then((result)=>{
        callback(result)
      })
    };
    const getChildren = () => {
      ajax(selected.value[0].id).then((result) => {
        let lastLevel = option.value.filter(item => item.id === selected.value[0].id)[0];
        Object.assign(lastLevel, {children: result});
      });
    };
    ajax(0).then((result) => {
      option.value = (result as any)
    });
    return {Demo,CascaderDemo2,CascaderDemo1,loadData,getChildren,Cascader,option,selected}
  }
};
</script>
