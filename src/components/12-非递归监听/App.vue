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
  1.递归监听存在的问题
  如果数据量比较大, 非常消耗性能

  2.非递归监听两个方法
  shallow【肤浅】Ref / shallowReactive

  3.如何触发非递归监听属性更新界面?
  如果是shallowRef类型数据, 可以通过triggerRef来触发

  4.应用场景
  一般情况下我们使用 ref和reactive即可
  只有在需要监听的数据量比较大的时候, 我们才使用shallowRef/shallowReactive
  * */
  import {shallowReactive} from 'vue';
  import {shallowRef, triggerRef} from 'vue';
export default {
  name: 'App',
  setup() {
    // let state = shallowReactive({
    let state = shallowRef({
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
        //
        //监听第一层，就更新UI，第一层的数据发送改变，下面也显示出来了
        // console.log(state);
        // console.log(state.gf);
        // console.log(state.gf.f);
        // console.log(state.gf.f.s);

        // state.value = {
        //     a:'1',
        //     gf:{
        //         b:'2',
        //         f:{
        //             c:'3',
        //             s:{
        //                 d:'4'
        //             }
        //         }
        //     }
        // }

        // state.value.a = '1';
        // state.value.gf.b = '2';
        // state.value.gf.f.c = '3';
        // state.value.gf.f.s.d = '4';

        state.value.gf.f.s.d = '4';
        // 注意点: Vue3只提供了triggerRef方法, 没有提供triggerReactive方法
        //        所以如果是reactive类型的数据, 那么是无法主动触发界面更新的
        //根据state中修改的数据来更新界面
        triggerRef(state);

        // 注意点: 如果是通过shallowRef创建数据,
        // 那么Vue监听的是.value的变化, 并不是第一层的变化
        //只有.value发送变化，才会主动更新界面
        console.log(state);
        console.log(state.value);
        console.log(state.value.gf);
        console.log(state.value.gf.f);
        console.log(state.value.gf.f.s);

    }
    return {state, myFn}
  }
}
</script>

<style>

</style>
