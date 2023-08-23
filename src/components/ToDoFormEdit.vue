<template>
  <div class="container form">
    <div class="addtask">
      <input
        type="text"
        class="input"
        placeholder="Update Task..."
        v-model="this.newMessage"
      />
      <button class="btn" :disabled="isDisabled" @click="updateTask">
        UPDATE
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["task"],
  data() {
    return {
      newMessage: "",
    };
  },
  computed: {
    isDisabled() {
      return this.newMessage.trim() === "";
    },
  },
  emits: ["updateTask"],
  methods: {
    updateTask() {
      this.task.message = this.newMessage;
      this.newMessage = "";
      this.task.isEdit = !this.task.isEdit;
      this.$emit("updateTask", this.task);
    },
  },
};
</script>

<style scoped>
.addtask {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 10px;
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
  padding: 9px 9px;
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
