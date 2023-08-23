<template>
  <div class="task">
    <input
      type="text"
      class="input"
      :value="task.message"
      readonly
      @click="isCompleted"
      :class="task.isCheck ? 'isCompleted' : ''"
    />
    <div class="icon">
      <i class="fa-sharp fa-regular fa-pen-to-square" @click="editing"></i>
      <i class="fa-sharp fa-solid fa-trash" @click="deleteTask"></i>
    </div>
  </div>

  <ToDoFormEdit
    v-if="formEditVisible"
    :task="this.task"
    @updateTask="handleEvent"
  ></ToDoFormEdit>
</template>

<script>
import ToDoFormEdit from "./ToDoFormEdit.vue";
export default {
  components: { ToDoFormEdit },
  props: ["task"],
  emits: ["deleteTask"],
  computed: {
    formEditVisible() {
      return this.task.isEdit; // Sử dụng task.isEdit để xác định có hiển thị form edit hay không
    },
  },
  methods: {
    isCompleted() {
      this.task.isCheck = !this.task.isCheck;
    },

    editing() {
      this.task.isEdit = !this.task.isEdit;
      // console.log(this.task.isEditEd);
    },

    handleEvent(updateTask) {
      this.task.isEdit = updateTask.isEdit;
      // console.log(this.task.isEdit);
    },

    deleteTask() {
      this.$emit("deleteTask", this.task);
      // console.log(this.task);
    },
  },
};
</script>

<style scoped>
.task {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 10px;
}

.task .input {
  width: calc(100% - 100px);
  outline: none;
  height: 100%;
  padding: 10px 20px;
  border: 1px solid #007cff;
  cursor: pointer;
  /* color: #fff; */
}

.icon {
  display: flex;
  height: 100%;
  gap: 10px;
  margin-right: 15px;
}

.icon i {
  cursor: pointer;
}

.isCompleted {
  text-decoration: line-through;
}
</style>
