<script setup lang="ts">
import { useSession } from '../models/session';
import { ref, reactive, onMounted } from 'vue';
import { User } from "../models/user";
import {usePosts } from "../models/posts";  
const session = useSession();

const users = usePosts();
users.fetchAllUsers();
const taa = [];
const currentTab= ref('All');
const newTaskName = ref('');
const dueDate = ref('');
const assignedTo = ref('');
const allTasks = ref(taa);
const tasks = ref(taa);
const assignedUser = ref(null as string | null | undefined);
//let tasks: Array<string>;
console.log('Haha users',users.users);
function addTask(){
        //const user = users.list.find(u => u.id+"" == assignedTo.value);
        //assignedUser.value = session.user?.handle
        //console.log(assignedUser);
        //console.log(user)
        allTasks.value.unshift({ 
          task: newTaskName.value,
          dueDate: dueDate.value,
          isCompleted: false,
        })
        console.log('Added new task')
        //tasks.value = allTasks;
        newTaskName.value = ''
        dueDate.value = ''
        assignedTo.value = ''       
}
function taskHandler( tab : string){
  currentTab.value = tab
  if (currentTab.value.includes('Current')) {
    tasks.value = allTasks.value.filter((task: any) => !task.isCompleted);
  }
  else if (currentTab.value.includes('Completed')) {
    tasks.value = allTasks.value.filter((task: any) => task.isCompleted);
  }
  else {
    tasks.value = allTasks.value;
  }
}
</script>

<template>
  <div class="section">
    <div class="container">
      <div class="columns">
        <div class="column">
          <div class="panel">
            <div class="tabs is-boxed">
              <ul>
                <li :class='{ "is-active": currentTab == "Current" }' @click="taskHandler('Current')">
                  <a>
                    <span class="icon ">
                      <i class="fas fa-clipboard-list" aria-hidden="true"></i>
                    </span>
                    <span>Current</span>
                  </a>
                </li>
                <li :class='{ "is-active": currentTab == "Completed" }' @click="taskHandler('Completed')">
                  <a>
                    <span class="icon ">
                      <i class="fas fa-calendar-times" aria-hidden="true"></i>
                    </span>
                    <span>Completed</span>
                  </a>
                </li>
                <li :class='{ "is-active": currentTab == "All" }' @click="taskHandler('All')">
                  <a>
                    <span class="icon ">
                      <i class="fas fa-calendar" aria-hidden="true"></i>
                    </span>
                    <span>All</span>
                  </a>
                </li>
              </ul>
            </div>
            <div class="panel-block">
              <form style="width: 100%;" @submit.prevent="addTask">
                <div class="field has-addons">
                  
                  <div class="card">
  <div class="card-content">
    <div class="control has-icons-left is-expanded">
                    <input class="input is-primary" type="text" placeholder="New Task" v-model="newTaskName" />
                    <span class="icon is-left">
                      <i class="fas fa-calendar-plus" aria-hidden="true"></i>
                    </span>
                  </div>
  </div>
</div>
                  <br>
                   <div class="card">
  <div class="card-content">
                  <div class="control has-icons-left is-expanded">
                    <input class="input is-primary" type="date" placeholder="Date" v-model="dueDate" />
                    <span class="icon is-left">
                      <i class="fa fa-dharmachakra" aria-hidden="true"></i>
                    </span>
                    </div>
                    </div>
                  </div><br>
                  <br>
                   <div class="card">
  <div class="card-content">
                  <div class="control">
                    <button class="button is-primary" style="width:100%">Add</button>
                  </div>
                  </div>
                  </div>
                </div>
              </form>
            </div>
            <!-- <a class="panel-block" >
              <input type="checkbox"/>
              <span></span>
            </a> -->
            <div class="cardstyles">
                 <div class="card" v-for="task in tasks" :key="task.title"> 
                    <div class="card-content">
                      <h1 class="completedheadtag">Mark as Completed?<a class="panel-block" :class="{ 'is-completed': currentTab != 'Completed' && task.isCompleted }"><input type="checkbox" v-model="task.isCompleted" /></a></h1>
                      <hr>
                      <h1 class="completedheadtag">Title of the task:<p>{{task.task}}</p></h1>
                      <hr>
                      <h1 class="completedheadtag">DueDate:<p>{{ task.dueDate }}</p></h1>
                      <hr>
                      <h1 class="completedheadtag">AssignedBy:<p>{{task.assignedBy}}</p></h1>
                        <div class="content">
                   </div>
                </div>
                </div>
</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
    .card{
      width: 30%;
      margin: 20px;
      
    }
    .cardstyles{
      display: flex;
      background-color: #F2D2BD;

    }
    .cardcontent h1{
      color:#FF0000;
    }
    .completedheadtag{
      display: flex;
      
    }
    .completedheadtag p{
      color: #b8860b;
    }
</style>
