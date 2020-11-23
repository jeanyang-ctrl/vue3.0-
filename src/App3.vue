// 05-vue2.0存在的问题
<template>
  <div>
    <form>
      <input type="text" v-model="stu.id">
      <input type="text" v-model="stu.name">
      <input type="text" v-model="stu.age">
      <input type="submit" @click="addStu">
    </form>
    <ul>
      <li v-for="(stu, index) in stus"
      :key="stu.id"
      @click="remStu(index)">
        {{stu.name}} -- {{stu.age}}
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  name: 'App',
  data:function () {
    return {
      stus:[
        {id:1, name:'zs', age:10},
        {id:2, name:'ls', age:20},
        {id:3, name:'ww', age:30},
      ],
      stu:{
        id:'',
        name:'',
        age:''
      }
      //vue2.0开发规律：
      // 新增功能1的数据
      // 新增功能2的数据
    }
  },
  methods:{
    remStu(index){
      this.stus = this.stus.filter((stu, idx) => idx !== index);
    },
    addStu(e){
      e.preventDefault();
      // 拷贝
      const stu = Object.assign({}, this.stu);
      this.stus.push(stu);
      this.stu.id='';
      this.stu.name='';
      this.stu.age='';
    }
    // 新增功能1的业务逻辑
    // 新增功能2的业务逻辑
  },
  computed:{
    // 新增功能1的业务逻辑
    // 新增功能2的业务逻辑
  },
  watch:{
    // 新增功能1的业务逻辑
    // 新增功能2的业务逻辑
  }
}
</script>

<style>
/* 造成的弊端是数据和逻辑分散了，不利于去管理和维护，
vue3.0为解决这个问题推出了组合API */
</style>
