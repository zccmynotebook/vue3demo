<template>
  <h1>{{ msg }}</h1>
  <h2>{{obj.name}}</h2>
  <button type="button" @click="count++">count is: {{ count }}</button>
  <button type="button" @click="changemsg">changemsg</button>
</template>
<script setup lang="ts">
import { ref,toRefs,reactive } from 'vue' 
 const state = reactive({
  foo: 1,
  bar: 2
})

const stateAsRefs = toRefs(state)
 
state.foo++
console.log('stateAsRefs',stateAsRefs) // 2

stateAsRefs.foo.value++
console.log('state',state)  


      const count = ref(0);
      let msg=ref(111)
      let obj=ref({name:'vue3'})
      function changemsg(){
        msg.value=222
      }
    
      console.log(count,msg)
      
</script>
 