<template>
  <div>
    <ul>
      <li class="py-3" v-for="(task, index) in tasks" :key="index">
        {{ task.name }} - {{ task.time }}
        <button
          class="btn btn-primary"
          @click="openEditForm(index)"
          data-bs-toggle="modal"
          data-bs-target="#staticBackdrop"
        >
          Edit
        </button>
      </li>
    </ul>

    <!-- modal -->

    <div
      class="modal fade"
      id="staticBackdrop"
      data-bs-backdrop="static"
      data-bs-keyboard="false"
      tabindex="-1"
      aria-labelledby="staticBackdropLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="staticBackdropLabel">
              Modal title
            </h1>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <form @submit.prevent="updateTask">
              <label for="editName">Name:</label>
              <input
              class="form-control my-2"
                v-model="editTask.name"
                type="text"
                id="editName"
                required
              />

              <label for="editTime">Time:</label>
              <input
              class="form-control my-2"
                v-model="editTask.time"
                type="number"
                id="editTime"
                required
              />

              <button type="submit" class="btn btn-primary">Update</button>
            </form>
          </div>
          <div class="modal-footer">
            <button
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
    <!-- <a class="btn btn-primary"  role="button">Open first modal</a> -->
  </div>
</template>

<script setup>
import { ref } from "vue";

const tasks = ref([
  { name: "Task 1", time: 30 },
  { name: "Task 2", time: 40 },
  { name: "Task 3", time: 60 },
  { name: "Task 4", time: 45 },
  { name: "Task 5", time: 50 },
]);

const showEditForm = ref(false);
const editTask = ref({ name: "", time: 0 });
let editingIndex = null;

const openEditForm = (index) => {
  editingIndex = index;
  editTask.value = { ...tasks.value[index] };
  showEditForm.value = true;
};

// const closeEditForm = () => {
//   showEditForm.value = false;
// };

const updateTask = () => {
  tasks.value[editingIndex] = { ...editTask.value };
  showEditForm.value = false;
};
</script>

<style>
ul li {
  list-style: none;
}
</style>
