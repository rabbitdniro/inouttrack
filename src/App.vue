<script setup>
import { ref } from 'vue';

const tasks = ref([
  {
    name: "Task 1",
    time: 30
  },
  {
    name: "Task 2",
    time: 40
  },
  {
    name: "Task 3",
    time: 60
  },
  {
    name: "Task 4",
    time: 45
  },
  {
    name: "Task 5",
    time: 50
  }
]);

// Take user input

const uname = ref("");
const utime = ref(0);

// Collecting Index when clicks edit button
const editIndex = ref();

const collectIndex = (ind) => {
  editIndex.value = ind;
}

// Edit Tasks Data
const editTasksData = (num) => {
  tasks.value[num].name = uname;
  tasks.value[num].time = utime;
}

 // Show Modal
 const showPopup = () => {
  modal.showModal();
 }

 // Close Modal
 const closePopup = () => {
  modal.close();
 }
</script>

<template>

  <div class="container">
    
    <h3 class="">Task Names and Time</h3>
    <hr />
    <ul class="list-group">
        <li v-for="(task, index) in tasks" :key="index" class="list-group-item d-flex justify-content-between align-items-start">
            <div class="me-3">{{ task }}</div>
            <div>
                <button @click="showPopup(); collectIndex(index)" class="btn-primary" type="button">Edit</button>
            </div>
        </li>
    </ul>

    <!-- Popup Dialog -->
    <dialog id="modal" style="border: none;">
        <div class="card">
            <form @submit.prevent action="">
                <div class="row mb-3 align-items-center">
                    <div class="input-group">
                        <div class="input-group-text"><strong>Name</strong></div>
                        <input v-model="uname" type="text" name="name" placeholder="Task 1" class="form-control">
                    </div>
                </div>

                <div class="row mb-3 align-items-center">
                    <div class="input-group">
                        <div class="input-group-text"><strong>Time</strong></div>
                        <input v-model="utime" type="number" name="time" placeholder="30" min="1" class="form-control">
                    </div>
                </div>

                <div class="row align-items-center">
                    <div class="col">
                        <button @click="editTasksData(editIndex); closePopup()" type="button" class="btn btn-primary">Submit</button>
                    </div>
                    <div class="col">
                        <button @click="closePopup()" type="button" class="btn btn-primary">Close</button>
                    </div>
                </div>
            </form>
        </div>
    </dialog>
  </div>
  
</template>

<style scoped>
 
</style>
