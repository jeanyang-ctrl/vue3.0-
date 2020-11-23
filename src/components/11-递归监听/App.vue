<template>
  <div>
      <p>{{state.a}}</p>
      <p>{{state.gf.b}}</p>
      <p>{{state.gf.f.c}}</p>
      <p>{{state.gf.f.s.d}}</p>
    <button @click="myFn">按钮</button>
  </div>
</template>

<script>
  /*
  1.递归监听
  默认情况下, 无论是通过ref还是reactive都是递归监听

  2.递归监听存在的问题
  如果数据量比较大,每一层都要递归包装成Proxy对象,非常消耗性能

  3.非递归监听
  * */
  import {reactive} from 'vue';
  // import {ref} from 'vue';
export default {
  name: 'App',
  setup() {
    let state = reactive({
      //无论你创建多少层，都可以内部递归监听，
      //修改每个层的数据都可以监听到
      //这是因为因为每一层都包装成Proxy对象
    // let state = ref({
        a:'a',
        gf:{
            b:'b',
            f:{
                c:'c',
                s:{
                    d:'d'
                }
            }
        }
    });
    function myFn() {
        // state.a = '1';
        // state.gf.b = '2';
        // state.gf.f.c = '3';
        // state.gf.f.s.d = '4';

// ref监听数据，＋.value
        // state.value.a = '1';
        // state.value.gf.b = '2';
        // state.value.gf.f.c = '3';
        // state.value.gf.f.s.d = '4';

        console.log(state);//第一层
        console.log(state.gf);//第二层
        console.log(state.gf.f);//第三层
        console.log(state.gf.f.s);//第四层
    }
    return {state, myFn}
  }
}
</script>

<style>

</style>
