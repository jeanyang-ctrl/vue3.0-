<template>
  <div ref="box">我是div</div>
</template>

<script>
  /*
  1.获取元素
  在Vue2.x中我们可以通过给元素添加ref='xxx',
  然后再代码中通过refs.xxx的方式来获取元素
  在Vue3.x中我们也可以通过ref来获取元素
  * */
  import {ref, onMounted} from 'vue';
export default {
  name: 'App',
  /*
    setup
  beforeCreate
  Created
  * */
//  在组合api中如何编写生命周期了？vue3.0把生命周期函数都抽取出去了
  setup() {
    // console.log(this.$refs.box);vue3.0是不能这样获取的
    let box = ref(null); // reactive({value: null})

//当界面挂载，自动渲染这个生命周期函数
    onMounted(()=>{
      console.log('onMounted',box.value);
    });

    console.log(box.value); // null

    return {box};
  }
}
</script>

<style>

</style>
