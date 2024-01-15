<template>
  <div>
    <div class="container py-5">
      <div class="pt-5" v-for="(task, index) in tasks" :key="index">
        <span>{{ task.name }} - {{ task.time }} minutes</span>
        <button class="btn btn-danger ms-3" @click="removeTask(index)">
          Remove
        </button>
      </div>

      <!-- <button class="btn btn-primary" @click="showPopup">Add Task</button> -->

      <button type="button" @click="showPopup" class="btn btn-primary">
        Add Task
      </button>

      <div v-if="isPopupVisible">
        <!-- Popup content for adding tasks -->
      </div>

      <!-- modal -->
      <div class="bg-light p-4 w-50 mt-3 rounded" v-show="isPopupVisible">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h1 class="modal-title fs-5" id="exampleModalLabel">
                Modal title
              </h1>
              <button
                @click="isPopupVisible = false"
                type="button"
                class="btn-close"
                data-bs-dismiss="modal"
                aria-label="Close"
              ></button>
            </div>
            <div class="modal-body">
              <input
                class="form-control mb-3"
                v-model="newTaskName"
                placeholder="Task name"
              />
              <input
                class="form-control mb-3"
                v-model.number="newTaskTime"
                placeholder="Task time"
              />
              <button @click="addTask" class="btn btn-primary">Add</button>
            </div>
            <div class="modal-footer">
              <button
                @click="isPopupVisible = false"
                type="button"
                class="btn btn-secondary"
                data-bs-dismiss="modal"
              >
                Close
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
const tasks = ref([
  { name: "Task 1", time: 60 },
  { name: "Task 2", time: 75 },
  // Add more initial tasks if needed
]);
const isPopupVisible = ref(false);
const newTaskName = ref("");
const newTaskTime = ref(0);

const showPopup = () => {
  isPopupVisible.value = true;
};

const addTask = () => {
  tasks.value.push({ name: newTaskName.value, time: newTaskTime.value });
  resetForm();
};

const removeTask = (index) => {
  tasks.value.splice(index, 1);
};

const resetForm = () => {
  newTaskName.value = "";
  newTaskTime.value = 0;
  isPopupVisible.value = false;
};
</script>
