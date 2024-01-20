<template>
 <div>
    <ul>
      <li class="py-3" v-for="(task, index) in tasks" :key="index">
        {{ task.name }} - {{ task.time }}
        <button class="btn btn-primary" @click="openEditForm(index)">Edit</button>
      </li>
    </ul>

    <!-- Edit Form Popup -->
    <div v-if="showEditForm">
      <form @submit.prevent="updateTask">
        <label for="editName">Name:</label>
        <input v-model="editTask.name" type="text" id="editName" required>

        <label for="editTime">Time:</label>
        <input v-model="editTask.time" type="number" id="editTime" required>

        <button type="submit">Update</button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

    const tasks = ref([
      { name: 'Task 1', time: 30 },
      { name: 'Task 2', time: 40 },
      { name: 'Task 3', time: 60 },
      { name: 'Task 4', time: 45 },
      { name: 'Task 5', time: 50 },
    ]);

    const showEditForm = ref(false);
    const editTask = ref({ name: '', time: 0 });
    let editingIndex = null;

    const openEditForm = (index) => {
      editingIndex = index;
      editTask.value = { ...tasks.value[index] };
      showEditForm.value = true;
    };

    const closeEditForm = () => {
      showEditForm.value = false;
    };

    const updateTask = () => {
      tasks.value[editingIndex] = { ...editTask.value };
      showEditForm.value = false;
    };


</script>


<style>
ul li{
  list-style: none;
}
</style>