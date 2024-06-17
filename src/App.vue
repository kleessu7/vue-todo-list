<script setup lang="ts">
import {ref} from 'vue'
// 定义响应式对象：
let todoText = ref<string>('');

// 将taskList中的内容传送到浏览器的存储空间以保存
// 描述该对象存放的是什么类型的：
let taskList = ref<{id:number, text:String, isDone:boolean}[]>([]);
  // {
  //   id: 1,
  //   text: '任务1',
  //   // true：打勾；false：不打勾
  //   isDone: false
  // },
  // {
  //   id: 2,
  //   text: '任务2',
  //   isDone: true
  // },
  // {
  //   id: 3,
  //   text: '任务3',
  //   isDone: false
  // }
// ]);

// 数据还原:
// 反串行化-将字符串解析为对象(在这里是数组)的形式:
taskList.value = JSON.parse(
    // 用key(taskList)去本地浏览器的储存空间拿出字符串:
    // 如果key(taskList)没有收到字符串,则用"[]"(字符串中只有空方括号,表示空数组)代替:
    // 所以必须要加上: ?? "[]"
    window.localStorage.getItem('taskList') ?? "[]"
);

function onAddTask(){
  taskList.value.push({
    id: taskList.value.length + 1,
    // 将添加的todoText文本作为任务名称
    text: todoText.value,
    isDone: false
  });
  todoText.value = '';

  // 数据持久化:
  // 将taskList中的内容传送到浏览器(换另一个浏览器就会消失)中的本地存储空间里（以字典的形式存储）：
  window.localStorage.setItem('taskList', JSON.stringify(taskList.value))   // key-value，value是字符串形式
  // 但我们存进去的不是字符串是数组，所以要对value进行串行化,将其转化为字符串
}
</script>

<template>
  <div class="container">

    <h1>ToDo List</h1>

    <div class="input-row">

      <el-input style="width: 20em" placeholder="请输入一个待办事项…" v-model="todoText"></el-input>

<!--      success：表示该button按钮的颜色为绿色，无其他含义，仅代表颜色-->
<!--      @click：一个点击事件-->
      <el-button type="success" @click="onAddTask">添加</el-button>

    </div>

    <div class="task-list">

<!--      v-for:循环任务，根据taskList中的对象个数进行循环-->
      <div v-for="item of taskList" class="task-item">

        <el-checkbox v-model="item.isDone" size="large">
          {{ item.text }}
        </el-checkbox>

        <div>
          <el-button type="primary">修改</el-button>
          <el-button type="danger">删除</el-button>
        </div>

      </div>

    </div>

  </div>
</template>【

<style scoped>
.container{
  display: flex;
  flex-direction: column;
  height: 100vh;
  width: 80%;
  margin: 0 auto;
  background-color: #F3F3F3;
}

h1{
  text-align: center;
  margin-top: 20px;
}

.input-row{
  display: flex;
  justify-content: center;
  margin-top: 20px;
  gap: 0.5em;
}

.task-list{
  padding: 0.2em;
}

.task-item{
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #CCC;
}
</style>
