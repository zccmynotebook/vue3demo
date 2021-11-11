<template> 
   <input @keyup.enter="add" class="form-control"/>
   <ul class="list-group">
      <li v-for="item in list" class="list-group-item"> 
        <label>
         <input type="checkbox" @change="changeStatus($event,item.id)" :checked="item.done"/> 
         {{item.name}}
        </label>
        <button type="button" 
         class="btn btn-danger pull-right"
         @click="deleteItem(item.id)">删除</button>
       </li>
   </ul>
   <footer>
      <label class="pull-left">
         <input type="checkbox" @change="checkAll" :disabled="!list.length" :checked="isCheckAll"/> 
         已完成{{finish}}个 / 总共{{list.length}}个
      </label>
         <!-- <button type="button" 
         class="btn btn-danger pull-right"
         @click="deleteDone">清除已完成</button> -->
   </footer>
</template>
<script setup>
import { nanoid } from 'nanoid'
import {reactive,ref, computed,toRefs,watch} from 'vue'
let name=ref('')
let list=reactive([])
let finish=ref(0)
let isCheckAll=ref(false)
watch(list,()=>{
   finish.value=list.filter(v=>v.done).length
   isCheckAll.value=finish.value===list.length
}) 
 
function add(e){
  let value=e.target.value.trim()
  if(value=='') return
  list.push({id:nanoid(),name:value,done:false})
  e.target.value=''
}
function deleteItem(id){
  let i=list.findIndex(v=>v.id===id)
  list.splice(i,1)
}
function changeStatus({target},id){
  list.forEach(v => {
     if(v.id===id) v.done=target.checked
  });
} 
 
function deleteDone(){
   list.forEach((v,i) => {
     if(v.done) list.splice(i,1)
   });
}
function checkAll({target:{checked}}){
   list.forEach((v,i) => {
     v.done=checked
   });
}
</script>
<style scoped>
ul{
   list-style: none;
    margin-top:10px;
    text-align: left;
}
 
</style>