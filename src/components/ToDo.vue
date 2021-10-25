<template>
  <div class="container">
    <h2 class="text-center">My To Do List</h2>
    <div class="d-flex">
    <input v-model= "task" type="text" placeholder="Enter Task" class="form-control">
    <button @click="submitTask" class="btn btn-warning rounded-0">Submit</button>
    </div>

<table class="table table-bordered mt-5">
  <thead class="thead-light">
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col">#</th>
      <th scope="col">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task,index) in tasks" :key="index">
      <th scope="row">{{task.name}}</th>
      <td style="width=120px;"><span @click="changeStatus(index)" class="pointer">{{task.status}}</span></td>
      <td><div @click="editTask(index)"><span class="fa fa-pen text-center"></span></div></td>
      <td><div @click="deleteTask(index)"><span class="fa fa-trash text-center"></span></div></td>
    </tr>

  </tbody>
</table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {
      task:'',
      taskEdit : null,
      availableStatuses:['to-do','in-progress','completed'],

      tasks:[{
        name:"Task 1",
        status:"pending"
      },{
        name:"Task 2",
        status:"pending"
      }]
    }
  },
  methods:{
   submitTask(){
     if(this.task === '') return;

     if(this.taskEdit === null){
     this.tasks.push({name:this.task,status:'to-do'})
     }else{
         this.tasks[this.taskEdit].name = this.task;
         
     }
     this.task='';
   },
   deleteTask(index){
        this.tasks.splice(index,1);
           this.task='';
   },
  editTask(index){
        this.task = this.tasks[index].name ;
        this.taskEdit = index;
    
   },
   changeStatus(index){
     let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
     if(++newIndex > 2 ){
       newIndex = 0;
     }
     this.tasks[index].status = this.availableStatuses[newIndex];
   }
  }
}
</script>
<style scoped>
.pointer{
  cursor :pointer;
}
</style>

