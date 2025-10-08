<script setup>
  
  // Imports
  import { reactive } from 'vue';

  // State
  const state = reactive({
  //   tasks: [
  //     { id: 1, title: 'Task 1', completed: false },
  //     { id: 2, title: 'Task 2', completed: true },
  //     { id: 3, title: 'Task 3', completed: false },
  //   ],
  //   newTask: '',
    filter: 'all', // all, pending, completed
      
      tasks: [ 
        {title: "task 1", completed: false},
        {title: "task 2", completed: true},
        {title: "task 3", completed: false}
      ],

      newTask: '',
  });

// Counter of tasks pending
  // Method 1
  function tasksDone(){
    let count = 0;
    state.tasks.forEach((task) => {
      if(!task.completed) count++;
    });
    return count;
  }
  // Method 2
  // const tasksPending = () => state.tasks.filter(task => task.title === "task 2").length;

  // Method 3
  const tasksPending = () => state.tasks.filter(task => !task.completed).length;

  // Method 4
  const getTasksPending = () => {
    return state.tasks.filter(tasks => !tasks.completed);
  }

  const getTasksCompleted = () => {
    return state.tasks.filter(tasks => tasks.completed);
  }

  const getTasksFiltered = () =>{
    const {filter} = state
    switch(filter){
      case 'pendentes':
        return getTasksPending();
      case 'completas':
        return getTasksCompleted();
      default:
        return state.tasks
    }
  }

  // Add new task
  const addTask = ( ) => {
    if(state.newTask.length >= 3) {
      const addNewTask = {
      title: state.newTask,
      completed: false
    };
    state.tasks.push(addNewTask);
    state.newTask = '';
    }else{
      alert('A tarefa deve ter no mínimo 3 caracteres.')
    }
  }

</script>

<template>
  <!-- <div class="container">
    <h1 class="text-center my-4">To-Do List</h1>
    <div class="input-group mb-3">
      <input type="text" class="form-control" placeholder="Add a new task" />
      <button class="btn btn-primary" type="button">Add</button>
    </div>
    <ul class="list-group">
      <li class="list-group-item d-flex justify-content-between align-items-center">
        Sample Task
        <button class="btn btn-danger btn-sm">Delete</button>
      </li>
    </ul>
  </div> -->

  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>Você tem {{ tasksDone()}} | {{ getTasksPending().length }} tarefas pendentes</p>
    </header>
  </div>
  <form @submit.prevent="addTask" action="">
    <div class="row">
      <div class="col">
        <input @change="e => state.newTask = e.target.value" required type="text" placeholder="Digite sua tarefa" class="form-control" v-bind:value="state.newTask">
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">ADD
        </button>
      </div>
      <div class="col-md-2">
        <select @change="e => state.filter = e.target.value" class="form-control" id="">
          <option value="todas">All Tasks</option>
          <option value="pendentes">Pending Tasks</option>
          <option value="completas">Completed Tasks</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="(tasks, index) in getTasksFiltered()">
      <input v-bind:checked="tasks.completed" :id="tasks.title" type="checkbox">
      <!-- <label :class="{ done: tasks.completed === !false}" class="ms-3" :for="tasks.title">{{ index + 1 }} : {{ tasks.title }}</label> -->
      <label :class="{ done: tasks.completed}" class="ms-3" :for="tasks.title">{{ index + 1 }} : {{ tasks.title }}</label>
    </li>
  </ul>
</template>

<style scoped>
  /* Add your styles here */
  .done{
    text-decoration: line-through;
    color: gray;
  }
</style>
