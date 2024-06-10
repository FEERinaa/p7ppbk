<template>
  <div class="todo-app">
    <h1>TODO LIST</h1>
    <form @submit.prevent="addTask">
      <input v-model="newTask" placeholder="Add a new task" />
      <button type="submit">Tambah</button>
    </form>
    <ul>
      <li v-for="(task, index) in tasks" :key="index" :class="{ completed: task.completed }">
        <input type="checkbox" v-model="task.completed" @change="toggleTaskCompletion(index)" />
        <span>{{ task.text }}</span>
        <button @click="removeTask(index)">Hapus</button>
      </li>
    </ul>
    <p>Total Tugas yang belum selesai: {{ incompleteTasksCount }}</p>
  </div>
</template>

<script>
import { ref, computed } from 'vue';
import { useTodoStore } from '../stores/todoStore';

export default {
  setup() {
    const todoStore = useTodoStore();
    const newTask = ref('');

    const addTask = () => {
      if (newTask.value.trim()) {
        todoStore.addTask(newTask.value.trim());
        newTask.value = '';
      }
    };

    const removeTask = (index) => {
      todoStore.removeTask(index);
    };

    const toggleTaskCompletion = (index) => {
      todoStore.toggleTaskCompletion(index);
    };

    return {
      newTask,
      tasks: computed(() => todoStore.tasks),
      addTask,
      removeTask,
      toggleTaskCompletion,
      incompleteTasksCount: computed(() => todoStore.incompleteTasksCount)
    };
  }
};
</script>

<style scoped>
.todo-app {
  max-width: 600px;
  margin: 2rem auto;
  padding: 1rem 2rem;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  font-family: 'Roboto', sans-serif;
}

h1 {
  text-align: center;
  color: #333;
}

form {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1.5rem;
}

input[type="text"] {
  flex: 1;
  padding: 0.5rem;
  margin-right: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1rem;
}

button {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  background-color: #007BFF;
  color: white;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #0056b3;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  padding: 0.5rem 0;
  border-bottom: 1px solid #eee;
}

li:last-child {
  border-bottom: none;
}

li.completed span {
  text-decoration: line-through;
  color: #999;
}

li input[type="checkbox"] {
  margin-right: 0.5rem;
}

li button {
  margin-left: auto;
  background: #dc3545;
  color: white;
  border: none;
  padding: 0.3rem 0.6rem;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

li button:hover {
  background-color: #c82333;
}

p {
  text-align: center;
  font-size: 1.1rem;
  color: #555;
  margin-top: 1.5rem;
}
</style>
