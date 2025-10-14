<script setup>

// Props to receive from parent component (App.vue)
const props = defineProps([
  'subAddTask',
  'eFilter',
  'eNewTask',
  'vNewTask'
])

  import { reactive } from 'vue';

    const state = reactive({
      newTask: '',
    });

</script>

<template>
  <form @submit.prevent="props.subAddTask" action="">
    
    <div class="row" id="div_Alert_"></div>
    <div class="row" >
      <div class="col">
        <input @change="props.eNewTask" required type="text" placeholder="Digite sua tarefa" class="form-control"
          v-bind:value="props.vNewTask">
      </div>
      
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">ADD
        </button>
      </div>

      <div class="col-md-2">
        <select @change="props.eFilter" class="form-control">
          <option value="todas">All Tasks</option>
          <option value="pendentes">Pending Tasks</option>
          <option value="completas">Completed Tasks</option>
        </select>
      </div>

    </div>
  </form>
</template>

<style setup></style>