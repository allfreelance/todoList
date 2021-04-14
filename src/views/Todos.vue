<template>
  <div class="container mx-auto">
    <h1 class="mt-8 text-2xl">Todos</h1>
    <div class="mt-3">
      <div class="grid md:grid-cols-12 gap-4 sm:grid-rows">
        <div class="col-span-6 space-y-4 overflow-y-auto px-1 order-2" style="height:500px">
          <div v-for="(todo, index) in todos" :key="index"
            class="p-8 bg-white shadow-md rounded flex items-center justify-between"
            :class="{'bg-green-500' : todo.isDone}"
            >
            <div>
              <div>{{ todo.text }}</div>
              <div class="text-gray-500 text-sm">{{ todo.createdAt.toString() }}</div>
            </div>
            <div class="space-x-2">
              <button class="px-2 text-red-600" title="Remove todo" 
                @click="deleteTask(index)"
              >&times;</button>
              <button class="px-2 text-green-600" title="Mark as done" 
                @click="doneTask(index)"
                v-if="!todo.isDone"
              >&check;</button>
              <button class="px-2 text-orange-600" title="Mark as undone" 
                @click="undoneTask(index)"
                v-else
              >&#8630;</button>
            </div>
          </div>
          <div v-if="todos.length === 0" class="px-8 py-16 bg-white text-gray-700 shadow-md rounded text-sm">
            You dont have any task to do
          </div>
        </div>
        
        <div class="col-span-6 order-1">
          <div class="p-8 bg-white shadow-md rounded">
            <h2 class="text-xl">Add a todo</h2>
            <input type="text" class="p-2 mt-4 border rounded w-full" 
              v-model="todoText"
              @keydown.enter="addTodo">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { defineComponent, reactive, ref } from 'vue';

export default defineComponent ({
  setup() {
    const todos = reactive([]);
    const todoText = ref('');
    
    function addTodo() {
      todos.unshift({
        text: todoText.value,
        createdAt: new Date().toString(),
        isDone: false
      });
        todoText.value = ''
    }
    
    function deleteTask(index) {
      if (!confirm('Are you sure?')) {
        return;
      }
      todos.splice(index,1)
    }
    
    function doneTask(index) {
      todos[index].isDone = true
    }
    
    function undoneTask(index) {
      todos[index].isDone = false
    }
    
    return {
      todos,
      todoText,
      addTodo,
      deleteTask,
      doneTask,
      undoneTask
    }
  }
})
</script>
<style>
  
</style>