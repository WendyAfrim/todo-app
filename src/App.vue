<template>
  <div class="w-full flex">
    <section id='input-area' class="m-auto w-1/2 px-4">
      <h1 class="text-2xl text-center font-semibold">{{ taskCount }} {{ taskCount < 2 ? "Task" : "Tasks" }}</h1>
      <!-- save input as a variable -->

      <form @submit.prevent>
        <input
        class="border-2 border-black rounded-md w-full text-center"
        v-model="newTask"
        >

        <!-- trigger action to add the task -->
        <button @click="addTaskHandler" class="border-2 border-black rounded-md px-8 mt-2 m-auto">Add task</button>
      </form>
    </section>
  </div>
  <TaskList  @toggleComplete="toggleCompleteHandler"  :tasks="tasks"/>
</template>

<script>
import TaskList from './components/TaskList.vue';

export default {
  name: 'App', 
  data() {
    return {
      newTask : " ",
      tasks: [],
    };
  },
  methods: {

    toggleCompleteHandler(i) {
      this.tasks[i].complete = !this.tasks[i].complete; 
      console.log('it worked ! ' + i + ' has been clicked')
    },

    addTaskHandler() {
      
      if(this.newTask === " ") return;

      this.tasks.push(this.newTaskObject);
      this.newTask = " ";
    },
  }, 
  computed: {

    taskCount() {
      return this.tasks.length;
    },

    newTaskObject() {
      return {
        id: this.tasks.length + 1,
        name: this.newTask,
        complete: false,
      }
    }
  },
  components: {
    TaskList,
  }
}
</script>

<style scoped>

</style>