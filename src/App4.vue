//06组合API上:怎么编写组合API？
// 这时候找到组件的JS代码，在这里面提供了setup函数
<template>
  <div>
    <!-- 在这里面可以自动监听count变量的变化 -->
    <p>{{ count }}</p>
    <button @click="myFn">按钮</button>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "App",
  // setup函数是组合API的入口函数，
  //但setup入口函数如何定义变量，监听变量的变化，如何让这个变量变化之后自动更新这个组件的UI
  setup() {
    //很简单，！！定义变量的第一个方式
    // let count = 0;
    //但是你这么做是无法监听这个变量的变化的，
    //那如果你想监听这个变量的变化，让这个变量变化之后自动更新这个组件的UI
    //这时候，！！定义变量的第二种方式，导入ref函数
    // 定义了一个名称叫做count变量, 这个变量的初始值是0
    // 这个变量发生改变之后, Vue会自动更新UI
    let count = ref(0);
    // 在组合API中, 如果想定义方法, 不用定义到methods中, 直接定义即可
    function myFn() {
      // alert(123);测试
      // console.log(count.value);得到count对象有个value值
      count.value += 1;
    }
    // 注意点:
    // 在组合API中定义的变量/方法, 要想在外界使用, 必须通过return {xxx, xxx}暴露出去
    return { count, myFn };
    //这个代码的含义就是把组合API中的count暴露给外界使用
  },
};
// 综上：入口函数定义的变量，外界不能使用
//好处是不要卸载data里面，不要写在methods里面
</script>

<style></style>
