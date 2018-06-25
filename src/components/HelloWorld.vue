<template>
  <div class="hello">
    <h1>{{ msg }} {{ arrP }}</h1>
    <Child @change='getVal'></Child>
  </div>
</template>


<script>
import Child from './child1'
  export default{
      components:{
          Child
      },
      data:function(){
        return{
          msg:'Update your data here.Page:',
          arrP:'1'
          }
      },
      methods:{
          getVal:function(val){
            this.arrP = val;
          }
        }
  }
</script>

<style>
  .hello h1{
      margin-bottom: 30px;
      top: 30px;
      bottom:30px;
  }
</style>
