<template>
  <div :class="'avatar flex justify-center items-center'">
    <div class="w-24 rounded-full">
      <img src="../assets/gif/wired-lineal-17-avatar-man-nodding.gif" />
    </div>
  </div>

  <div class="max-w-md mx-auto mt-10 text-center">
    <h1 class="text-2xl font-semibold mb-4">To-Do List {{ newTask }}</h1>
    <div class="flex space-x-2">
      <input
        v-model="newTask"
        @keydown.enter="addTask"
        class="w-full rounded-md p-2 border border-gray-300 focus:ring focus:ring-blue-200"
        type="text"
        placeholder="Add a new task..."
      />
      <button
        @click="addTask"
        class="px-4 py-2 text-white bg-blue-500 rounded-full hover:bg-blue-600"
      >
        Add
      </button>
    </div>

    <div v-for="(task, index) in tasks" :key="index">
      <div v-if="task.completed">
        {{ task.text }}
      </div>
    </div>

    <ul class="mt-4">
      <li
        v-for="(task, index) in tasks"
        :key="index"
        class="flex justify-between items-center p-2 border-b border-gray-300"
        :class="{ 'bg-green-500': task.completed, 'bg-red-500': !task.completed }"
      >
        <input type="checkbox" class="mr-2" v-model="task.completed" />
        <span :class="{ 'line-through': task.completed }">{{ task.text }}</span>
        <span class="text-gray-500 text-sm">{{ task.timestamp }}</span>
        <button
          @click="removeTask(index)"
          class="text-white bg-red-500 hover:bg-red-600 px-2 py-1 rounded-md"
        >
          Delete
        </button>
      </li>
    </ul>
    <div class="flex justify-between items-center mt-4">
      <!-- <button
        v-if="isEmptyTasks()"
        @click="selectAllTasks"
        class="px-4 py-2 text-white bg-green-500 rounded-md hover:bg-green-600"
      >
        Select All
      </button> -->
      <ButtonComponent
        v-if="isEmptyTasks()"
        @click="selectAllTasks"
        buttonName="Select All"
        btnColor="success"
      />
      <!-- <button
        v-if="isEmptyTasks()"
        @click="toggleBlueButton"
        class="px-4 py-2 text-white bg-blue-500 rounded-md hover:bg-blue-600"
      >
        confirm
      </button> -->
      <ButtonComponent
        v-if="isEmptyTasks()"
        @click="toggleBlueButton"
        buttonName="confirm"
        btnColor="primary"
      />
      <button
        @click="deleteAllTasks"
        v-show="tasks.length > 0"
        class="px-4 py-[100px] text-white bg-[#42de1b] rounded-md hover:bg-red-600"
      >
        Delete All
      </button>
    </div>

    <!-- <ButtonComponent buttonName="????" btnColor="warning" /> -->
    <!-- <ButtonComponent buttonName="confirm" buttonClass="bg-blue-500 hover:bg-green-600" />
    <ButtonComponent buttonName="Delete All" buttonClass="bg-red-500 hover:bg-green-600" />
    <ButtonComponent buttonName="????" buttonClass="bg-yellow-500 hover:bg-green-600" /> -->
  </div>
</template>

<script setup>
import { ref } from 'vue'
import ButtonComponent from '../components/ButtonComponent.vue'

const newTask = ref('')
const tasks = ref([])
// const selectAll = ref(false)
const showBlueButton = ref(false)

const addTask = () => {
  if (newTask.value.trim() == '') {
    console.log('ค่าว่าง')
  } else {
    const timestamp = new Date().toLocaleString() // Get the current timestamp
    console.log(' work')

    let data = { text: newTask.value, completed: false, timestamp }
    tasks.value.push(data)
    newTask.value = ''
  }

  // console.log(newTask.value.trim() !== '')

  // if (newTask.value.trim() !== '') {
  //   console.log(newTask.value.trim())
  //   const timestamp = new Date().toLocaleString() // Get the current timestamp
  //   console.log(timestamp)

  //   let data = { text: newTask.value, completed: false, timestamp }
  //   tasks.value.push(data)
  //   newTask.value = ''
  // }
}

const removeTask = (index) => {
  tasks.value.splice(index, 1)
}

const deleteAllTasks = () => {
  tasks.value = []
}

const selectAllTasks = () => {
  const allCompleted = tasks.value.every((task) => task.completed)
  tasks.value.forEach((task) => (task.completed = !allCompleted))
}

const toggleBlueButton = () => {
  showBlueButton.value = !showBlueButton.value
}

// const formatDate = (timestamp) => {
//   // Format the timestamp as needed
//   return timestamp
// }

const isEmptyTasks = () => {
  return tasks.value.length !== 0
}
</script>

<style scoped>
/* Add your Tailwind CSS classes here if needed */

.nclass {
  background-color: brown;
}
</style>
