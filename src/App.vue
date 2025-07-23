<script setup>
import { ref } from 'vue';

// 初始化待办事项列表
const todos = ref([
  { id: 1, text: '学习Vue基础', completed: false },
  { id: 2, text: '创建第一个To-Do应用', completed: true }
]);
// 新任务输入框绑定
const newTodoText = ref('');
// 生成唯一ID
let nextId = 3;

// 添加新任务
const addTodo = () => {
  if (newTodoText.value.trim()) {
    todos.value.push({
      id: nextId++,
      text: newTodoText.value.trim(),
      completed: false
    });
    newTodoText.value = '';
  }
};

// 切换任务完成状态
const toggleTodo = (id) => {
  const todo = todos.value.find(t => t.id === id);
  if (todo) {
    todo.completed = !todo.completed;
  }
};

// 删除任务
const deleteTodo = (id) => {
  todos.value = todos.value.filter(t => t.id !== id);
};
</script>

<template>
  <div class="todo-app">
    <div class="logo-container">
        <img src="/todo-logo.svg" alt="Todo Logo" class="todo-logo" />
      </div>
      <h1>To-Do List</h1>
    <div class="todo-input-container">
      <input
        v-model="newTodoText"
        @keyup.enter="addTodo"
        placeholder="添加新的任务..."
        class="todo-input"
      />
      <button @click="addTodo" class="add-button">添加</button>
    </div>
    <ul class="todo-list">
      <li v-for="todo in todos" :key="todo.id" class="todo-item">
        <label class="todo-checkbox-container">
          <input
            type="checkbox"
            v-model="todo.completed"
          />
          <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        </label>
        <button
          @click="deleteTodo(todo.id)"
          class="delete-button"
          aria-label="删除任务"
        >
          ×
        </button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.todo-app {
  max-width: 500px;
  margin: 2rem auto;
  padding: 0 1rem;
  font-family: 'Arial', sans-serif;
}

.logo-container {
  display: flex;
  justify-content: center;
  margin-bottom: 1rem;
}

.todo-logo {
  width: 40px;
  height: 40px;
}

h1 {
  color: #333;
  text-align: center;
  margin-bottom: 2rem;
}

.todo-input-container {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.todo-input {
  flex: 1;
  padding: 0.75rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 1rem;
}

.add-button {
  padding: 0.75rem 1.5rem;
  background-color: #42b883;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.add-button:hover {
  background-color: #359e75;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.75rem;
  border-bottom: 1px solid #eee;
  transition: background-color 0.2s;
}

.todo-item:hover {
  background-color: #f9f9f9;
}

.todo-checkbox-container {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
}

.completed {
  text-decoration: line-through;
  color: #888;
}

.delete-button {
  background: none;
  border: none;
  color: #ff4444;
  font-size: 1.2rem;
  cursor: pointer;
  padding: 0.25rem;
  opacity: 0.7;
  transition: opacity 0.2s;
}

.delete-button:hover {
  opacity: 1;
}
</style>
