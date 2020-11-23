<template>
  <div>
    <ul>
      <li
        v-for="(stu, index) in state.stus"
        :key="stu.id"
        @click="remStu(index)"
      >
        {{ stu.name }} - {{ stu.age }}
      </li>
    </ul>
  </div>
</template>
// 07组合API中-理解
<script>
import { reactive } from "vue";
export default {
  name: "App",
  setup() {
    /*
    // ref函数注意点:
    // ref函数只能监听简单类型的变化, 不能监听复杂类型的变化(对象/数组)
    //vue3.0提供了个reactive方法，可以监听复杂类型数据的变化
    //这个方法接收一个对象，对象里面可以放上你监听数据-stu数组的变化
    let state = reactive({
      stus:[
        {id:1, name:'zs', age:10},
        {id:2, name:'ls', age:20},
        {id:3, name:'ww', age:30},
      ]
    });
    function remStu(index) {
      //现在访问的不是this.stu了，而是state.stu
    xxx this.stus = this.stus.filter((stu, idx) => idx !== index);

    √√√ state.stus = state.stus.filter((stu, idx) => idx !== index);
    }
     */

    // 解决了上述问题之后，我们看一下组合API是怎么组合的？
    let { state, remStu } = useRemoveStudent();
    return { state1, remStu };
  },
};

//写在外面的，向外暴露state, remStu，之后在setup函数导入变量函数即可
//则vue3.0的数据-业务逻辑不分散了
function useRemoveStudent() {
  let state = reactive({
    stus: [
      { id: 1, name: "zs", age: 10 },
      { id: 2, name: "ls", age: 20 },
      { id: 3, name: "ww", age: 30 },
    ],
  });
  function remStu(index) {
    state.stus = state.stus.filter((stu, idx) => idx !== index);
  }
  //暴露出去，供外界使用
  return { state, remStu };
}
</script>

<style></style>
