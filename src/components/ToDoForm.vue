<template>
  <div class="container form">
    <h1 class="title">To Do App</h1>

    <div class="addtask">
      <input
        v-model="this.task.message"
        type="text"
        class="input"
        placeholder="New Task..."
      />
      <button class="btn" @click="this.addNewTask" :disabled="isDisabled">
        ADD
      </button>
    </div>

    <div class="task">
      <ToDoTask
        v-for="task in data"
        :key="task.id"
        :task="task"
        @deleteTask="onDeleteTask"
      ></ToDoTask>
    </div>
  </div>
</template>

<script>
import ToDoTask from "./ToDoTask.vue";
import { v4 as uuidv4 } from "uuid";
export default {
  components: { ToDoTask },
  props: ["data", "addTask"],
  emits: ["deleteTask"],
  computed: {
    isDisabled() {
      return this.task.message.trim() === "";
    },
  },
  data() {
    return {
      task: {
        id: "",
        message: "",
        isEdit: false,
        isDelete: false,
        isCheck: false,
      },
    };
  },
  methods: {
    addNewTask() {
      const newTask = {
        id: "",
        message: this.task.message,
        isEdit: false,
        isDelete: false,
        isCheck: false,
      };
      newTask.id = uuidv4();
      this.addTask(newTask);
      //   console.log(newTask);
      this.task.message = "";
    },

    onDeleteTask(taskToDelete) {
      // Phát ra sự kiện mới để truyền lên component cha
      this.$emit("deleteTask", taskToDelete);
    },
  },
};
</script>

<style scoped>
.container {
  background-color: #fff;
  width: 500px;
  max-width: calc(100% - 50px);
  height: min-content;
  padding: 20px;
  margin: 10px;
  color: #007cff;
}

.addtask {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form .title {
  text-align: center;
  margin-bottom: 20px;
}

.addtask .input {
  width: calc(100% - 100px);
  outline: none;
  height: 100%;
  padding: 10px 20px;
  border: 1px solid #007cff;
}

.addtask .btn {
  background-color: #007cff;
  color: #fff;
  border: none;
  padding: 9px 20px;
  cursor: pointer;
  font-size: 100%;
  height: 100%;
}

.task {
  /* background-color: red; */
  /* height: 50px; */
  margin-top: 10px;
}
</style>
