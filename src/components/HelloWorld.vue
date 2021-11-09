<template>
  <h1>{{ msg }}</h1>
  <button type="button" @click="count++">count is: {{ count }}</button>
  
</template>
<script  lang="ts">
 import { ref } from 'vue'
export default {
  data(){
    console.log(this)
    return {b:2}
  },
    setup(){ 
      const count = ref(0);
      let msg=111
      console.log(this)
      return {msg,count}
  }
}
</script>
 