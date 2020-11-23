<template>
  <div>
    <p>{{name}}</p>
    <button @click="myFn1">按钮</button>
    <p>{{age}}</p>
    <button @click="myFn2">按钮</button>
  </div>
</template>

<script>
  /*
  1.Composition API 和Option API混合使用
  2.Composition API本质 (组合API/注入API)
  3.setup执行时机
  4.setup注意点
  * */

/*
  1.Option API即使在vue2.x当中添加的可选配置，
  在data定义一些数据，在methods定义方法
  data、methods就是Option API：
  data: function(){
    return {
      name: 'lnj',
      // age: 18
    }
  },
  methods:{
    myFn1(){
      alert('abc');
    },
  * */
/*
 * */
/*
  2. Composition API ：不管三七二十一，从vue导入ref函数，
  在setup入口函数定义一个变量age等于ref，默认初始值为18
  设完之后再定义一个myFn2方法，默认情况下外界不能使用，必须用给return暴露
 setup() {
    let age = ref(18);
    function myFn2() {
      alert('www.it666.com');
    }
    return {age, myFn2}
  }
  综上  Composition API 和Option API可以混合使用
 * */
  import {ref} from 'vue';
export default {
  name: 'App',
  data: function(){
    return {
      name: 'lnj',
      // age: 18
    }
  },
  methods:{
    myFn1(){
      alert('abc');
    },
    // myFn2() {
    //   alert('www.it666.com');
    // }
  },
  setup() {
    let age = ref(18);
    function myFn2() {
      alert('www.it666.com');
    }
    return {age, myFn2}
  }
}
</script>

<style>

</style>
/*
  2.Composition API本质 (翻译成组合API/注入API)
  本质是在运行的时候，将Composition API中暴露出去的数据
  注入到Option API

 * */