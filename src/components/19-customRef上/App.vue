<template>
  <div>
    <p>{{age}}</p>
    <button @click="myFn">按钮</button>
  </div>
</template>

<script>
  /*如何自定义ref，实际上自定义一个ref的方法
  1.customRef
  返回一个ref对象,可以显式地控制依赖追踪和触发响应
  * */
 //导入一个customref
  import {ref, customRef} from 'vue';

function myRef(value) {
  //导出一个customref
  return customRef((track, trigger)=>{
    return {
      get(){
        track(); // 告诉Vue这个数据是需要追踪变化的
        console.log('get', value);
        return value;
      },
      set(newValue){
        console.log('set', newValue);
        value = newValue;
        trigger(); // 告诉Vue触发界面更新
      }
    }
  });
}
export default {
  name: 'App',
  setup() {
    // let age = ref(18); // reactive({value: 18})
    let age = myRef(18);
    function myFn() {
      age.value += 1;
    }
    return {age, myFn}
  }
}
</script>

<style>

</style>
