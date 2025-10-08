<script setup>
  const props = defineProps([
    'tasksDone',
    'getTasksPending',
    'allTasks'
  ]);
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
  
   <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>Você tem {{ props.getTasksPending }} de  {{props.allTasks() }} tarefas pendentes</p>
    </header> 
</template>

<style setup>

</style>