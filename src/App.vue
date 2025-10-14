<script setup>
  
  // Imports
  import { reactive } from 'vue';
  import TaskList from './components/TaskList.vue';
  import Header_TD from './components/Header_TD.vue';
  import Form_TD from './components/Form_TD.vue';

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
        // {title: "task 1", completed: false},
        // {title: "task 2", completed: false},
        // {title: "task 3", completed: false}
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

  // alert message liveral
  const live_message = (msg) => {
    const alert_ = document.getElementById('div_Alert_');
    const message = document.createElement('div');
       message.innerHTML = [
        `<div class="alert alert-danger" role="alert" id="alert_">${msg}`,
      '</div>'
      ].join('');

      alert_.append(message);

      setTimeout(() => message.remove(), 5000)
  }

  const rm_live_message = () => {
    const alert_ = document.getElementById('alert_');
    console.log(alert_);
    
    if(alert_){
      alert_.remove();
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

    rm_live_message();

    }else{
      // alert('A tarefa deve ter no mínimo 3 caracteres.')
      
      live_message('A tarefa deve ter no mínimo 300 caracteres.')
    }
  }

  const allTasks = () => {
    return state.tasks.length;
  }

</script>

<template>
  

  <div class="container">
    <Header_TD :all-tasks="allTasks" :tasks-done="tasksDone()" :get-tasks-pending="getTasksPending().length "/>
   
    <Form_TD :sub-add-task="addTask" :e-filter="e => state.filter = e.target.value" :e-new-task="e => state.newTask = e.target.value" :v-new-task="state.newTask"/>
   
    <TaskList :get-tasks-filtered="getTasksFiltered()" />

  </div>
  
</template>

<style scoped>
  
</style>
