<template>
  <div>
    <p>{{state.time}}</p>
    <button @click="myFn">按钮</button>
  </div>
</template>

<script>
  /*
  1.什么是reactive?
    - reactive是Vue3中提供的实现响应式数据的方法
    - 在Vue2中响应式数据是通过defineProperty来实现的
      而在Vue3中响应式数据是通过ES6的Proxy来实现的
  2.reactive注意点:
    - reactive参数必须是自定义对象和array(json/arr)
    - 如果给reactive传递了其它对象
      + 默认情况下修改对象, 界面不会自动更新
      + 如果想更新, 可以通过重新赋值的方式
  * */
  import {reactive} from 'vue';
export default {
  name: 'App',
  setup() {
    // 创建一个响应式数据
    // 本质: 就是将传入的数据包装成一个Proxy对象
    // let state = reactive(123);vue并没有把它包装成一个Proxy对象+
    // let state = reactive({
    //   age: 123
    // });
    // let state1 = reactive([1, 3, 5]);
    let state = reactive({
      time: new Date() //创建一个时间对象
    });
    function myFn() {
      // state = 666; // +验证说法：这时候数据改了界面没改，由于在创建响应式数据的时候传递的不是一个对象, 所以无法实现响应式
      // state.age = 666; //这时候数据改了界面也改  响应式
      // console.log(state1)  //包装proxy对象，打印信息proxy{0：1，1：3，2：5}
      // state1[0] = 666; 
      // 2.直接修改以前的, 界面不会更新
      // state.time.setDate(state.time.getDate() + 1);
      //state.time.getDate() + 1拿到过去的时间天＋1 这样的话界面没改，数据改了
      // 重新赋值
      const newTime = new Date(state.time.getTime());//以当前的时间创建一个对象
      //把新的时间增加一天
      newTime.setDate(state.time.getDate() + 1);
      state.time = newTime;
      console.log(state.time);//数据界面发送变化
    }
    return {state, myFn};
  }
}
</script>

<style>

</style>
