<script setup lang="ts">
import {ref} from 'vue'

let todoText = ref<string>('');

let taskList = ref([{
    id: 1,
    text: '任务1',
    // true：打勾；false：不打勾
    isDone: false
  },
  {
    id: 2,
    text: '任务2',
    isDone: false
  },
  {
    id: 3,
    text: '任务3',
    isDone: false
  }
  ]);

function onAddTask(){
  taskList.value.push({
    id: taskList.value.length + 1,
    // 将添加的todoText文本作为任务名称
    text: todoText.value,
    isDone: false
  });
  todoText.value = '';
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
</template>

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
