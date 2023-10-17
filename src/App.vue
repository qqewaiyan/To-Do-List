<template>
  
 <div class="">
    <h3 class="text-center bg-primary text-white p-3">To Do list</h3>
    <div class="container">
        <div class="row">
            <div class="col">
                <input type="text" name="" class="form-control" id="" v-model="newTasks" v-on:keyup.enter="addTasks()">
            </div>
            <div class="col">
                <input type="button" class="btn btn-secondary" value="Add" v-on:click="addTasks()" >
            </div>
            <div class="col">
                <button class="btn btn-warning" @click="deleteTasks()">Delete Tasks</button>
            </div>
        </div>
        <div class="" v-if="filterTask.length >0">
            <div class="row fs-3 mb-3">
            <div class="col">
                Task
            </div>
            <div class="col-2">
                done
            </div>
        </div>
        <div class="row" v-for="(task,index) in filterTask" v-bind:key="index">
            <div class="col" :class=" task.done ? 'delete' : '' ">
                {{ task.action }}
            </div>
            <div class="col-2">
                <input type="checkbox" name="" v-model="task.done" id="">
            </div>
        </div>
        
        </div>
        <div class="alert alert-warning text-center mt-4" v-else>
            There is no data
        </div>
        <div class="bg-danger text-center p-2 row text-white">
            <h5 class="col">Hide Complete</h5>
            <input type="checkbox" name="" v-model="hideComplete"  id="">
            
        </div>
    </div>
 </div>
 
</template>

<script>
    export default{
        name : "APP",
        data : () => ({
            name : "CODE LAB",
            hideComplete : false,
            newTasks : "",
            tasks : []
        }),
       computed : {
        filterTask(){
        return this.hideComplete
        ? this.tasks.filter((v)=> !v.done) 
        : this.tasks;
       },
       },
       methods: {
        addTasks(){
            if(this.newTasks === ""){
                return   alert("Please add something")
            }
            
                this.tasks.push({
                action : this.newTasks,
                done : false,
            })
            this.storeData();

           this.newTasks = "";
            
        },
        deleteTasks(){
            
            this.tasks = this.tasks.filter((v) => !v.done);
            this.storeData();
        },
        storeData(){
            localStorage.setItem("myLocalTask",JSON.stringify(this.tasks));
        },
       },
       mounted() {
        
         let data =   localStorage.getItem("myLocalTask");
        if(data !== null){
            this.tasks = JSON.parse(data);
        }
        },
    }
</script>

<style>
    .delete{
        text-decoration: line-through;
    }
</style>
