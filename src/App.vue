<template>
  <div id="app" class="app-container">
    <h1 class="title">To-Do List App</h1>
    <input
      class="task-input"
      v-model="newTask"
      @keyup.enter="addTask"
      placeholder="Tambahkan tugas baru..."
    />
    <ul class="task-list">
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        {{ task.text }}
        <button class="edit-btn" @click="editTask(index)">Edit</button>
        <button class="delete-btn" @click="deleteTask(index)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const tasks = ref([]);
    const newTask = ref("");

    const addTask = () => {
      if (newTask.value.trim()) {
        tasks.value.push({ text: newTask.value });
        newTask.value = "";
      }
    };

    const deleteTask = (index) => {
      tasks.value.splice(index, 1);
    };

    const editTask = (index) => {
      const updatedTask = prompt("Edit Tugas:", tasks.value[index].text);
      if (updatedTask !== null) {
        tasks.value[index].text = updatedTask;
      }
    };

    return { tasks, newTask, addTask, deleteTask, editTask };
  },
};
</script>

<style scoped>
.app-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f4f4f9;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}
.title {
  color: #333;
  text-align: center;
}
.task-input {
  width: 100%;
  padding: 12px 10px;
  margin-bottom: 20px;
  border: 2px solid #ccc;
  border-radius: 4px;
}
.task-list {
  list-style: none;
  padding: 0;
}
.task-item {
  background-color: #fff;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
}
.edit-btn,
.delete-btn {
  margin-left: 10px;
  padding: 5px 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.edit-btn {
  background-color: #ffc107;
}
.delete-btn {
  background-color: #dc3545;
  color: #fff;
}
</style>
