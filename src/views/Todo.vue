<template>
  <div class="home">

    <list-tasks
        v-if="$store.state.tasks.length"
    ></list-tasks>
    <no-tasks
        v-else
    >
    </no-tasks>
    <button-done-sorting
    v-if="$store.state.sorting"
    />
  </div>
</template>

<script>
import FieldAddTask from "@/components/Todo/FieldAddTask.vue";
import ListTasks from "@/components/Todo/ListTasks";
import NoTasks from "@/components/Todo/NoTasks";
import ButtonDoneSorting from "@/components/Todo/ButtonDoneSorting";

  export default {
    name: 'Home',
    components: {
      'list-tasks': ListTasks,
      'no-tasks': NoTasks,
      'button-done-sorting': ButtonDoneSorting
    }

  }
</script>

