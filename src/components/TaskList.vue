<script setup>
const props = defineProps([
    'getTasksFiltered',
    'iceTasksCompleted',
    'ichTasksCompleted',
    'tasksTitle'
])
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="(tasks, index) in props.getTasksFiltered">
            <input @change="e => tasks.completed = e.target.checked" :checked="tasks.completed" :id="tasks.title" type="checkbox">
            <!-- <label :class="{ done: tasks.completed === !false}" class="ms-3" :for="tasks.title">{{ index + 1 }} : {{ tasks.title }}</label> -->
            <label :class="{ done: tasks.completed }" class="ms-3" :for="tasks.title">
                {{ index + 1 }} : {{ tasks.title
            }}
            </label>
        </li>
    </ul>
</template>

<style setup>
    /* Add your styles here */
  .done{
    text-decoration: line-through;
    color: gray;
  }
</style>