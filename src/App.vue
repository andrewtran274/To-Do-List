<template>
  <div class="wrapper">
    <ToDoForm
      :data="data"
      :addTask="this.addTask"
      @deleteTask="deleteTask"
    ></ToDoForm>
  </div>
</template>

<script>
import ToDoForm from "./components/ToDoForm.vue";
import { v4 as uuidv4 } from "uuid";

export default {
  components: { ToDoForm },
  data() {
    return {
      data: [],
    };
  },

  methods: {
    addTask(task) {
      this.data.push(task);
      // console.log(task);
    },

    deleteTask(taskToDelete) {
      const index = this.data.findIndex((task) => task.id === taskToDelete.id);

      if (index !== -1) {
        this.data.splice(index, 1);
      }
      console.log(this.data);
    },
  },
};
</script>

<style scoped>
.wrapper {
  width: 100%;
  height: 100vh;
  background-color: #00a7ff;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
