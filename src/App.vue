<template>
  <div class="container">
    <h2 class="text-center mt-5">To-do List</h2>

    <div class="d-flex">
          <input v-model="task" type="text" class="form-control">
          <button @click="submitTask" v-on:keyup.enter="submitTask" class="btn btn-warning rounded-0">Enregistrer</button>
    </div>

    <table class="table mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <th> {{task.name}} </th>
          <td style="width: 120px;">
            <span @click="changeStatus(index)" class="pointer"> {{task.status}} </span>
          </td>
          <td class="text-center" @click="editTask(index)">
            <div>
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td class="text-center" @click="deleteTask(index)">
            <div>
              <span class="fa fa-trash"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>


</template>

<script>
export default {
 name: 'Todo App',

 data() {
    return {
      task : '',
      editedTask: null,
      availableStatus: ['to-do', 'in progress', 'completed'],
      tasks: [{
        name: "Eat chocolate",
        status: "in-progress"
      }]
    }
 },

 methods: {

  submitTask() {
    if(this.task.length === 0) return; 

    if(this.editedTask === null) {
        this.tasks.push({
        name: this.task,
        status: 'to do'
      });
    } else {
      this.tasks[this.editedTask].name = this.task;
      this.editedTask = null;
    }

    this.task = " ";
  },

  deleteTask(index) {
    this.tasks.splice(index, 1);
  },

  editTask(index) {
    this.task = this.tasks[index].name
    this.editedTask = index;

  }, 
  
  changeStatus(index) {
    let newIndex = this.availableStatus.indexOf(this.tasks[index].status);
    if(++newIndex > 2) newIndex = 0;
    this.tasks[index].status = this.availableStatus[newIndex];
  }
 }

}
</script>

<style scoped>
  .pointer {
    cursor: pointer;
  }
</style>