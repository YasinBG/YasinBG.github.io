<template>
  <div class="flex flex-col justify-center mx-auto">
    <h2 class="text-3xl text-green-300 mx-auto my-8">Todo-List Uygulamasi</h2>
    <input 
      class="w-80 h-12 border-2 border-green-500 rounded mx-auto font-semibold"
      :value="newTask"
      @input="updateNewTask"
      @keyup.enter="addTask"
      placeholder=" Görev Ekle..."
    />
      <div class="mx-auto">
    <ul class="flex justify-center flex-col my-6" v-for="(task, index) in tasks" :key="index">
      <li class="flex justify-center mx-auto font-semibold">
        <input class="fixed mr-32 w-6 h-6 " type="checkbox" @change="completeTask(index)" :checked="task.completed" />
        <span class="mx-2" :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">
          {{ truncateText(task.baslik, 20) }}
        </span>
        <div class="fixed ml-60">
          <button
            @click="deleteTask(index)"
            class="border-red-800 border-2 text-center uppercase rounded bg-red-400 text-white w-12 h-6 font-semibold"
          >
            sil
          </button>
        </div>
      </li>
    </ul>
  </div>
    <button
      @click="recoverTask"
      class="mx-auto my-6 p-2 font-semibold border-2 border-green-600 text-center uppercase rounded bg-green-400 text-white hover:bg-green-600 w-24 h-10"
    >
      geri al
    </button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'HomeView',
  setup() {
    const tasks = ref([{ baslik: 'Ornek Task', completed: false }]);

    const newTask = ref('');

    const deletedTasks = ref([]);

    const addTask = () => {
      tasks.value.push({ baslik: newTask.value.trim(), completed: false });
      newTask.value = '';
    };

    const deleteTask = (index) => {
      const deletedTask = tasks.value.splice(index, 1)[0];
      deletedTasks.value.unshift(deletedTask);
    };

    const recoverTask = () => {
      if (deletedTasks.value.length > 0) {
        const recoveredTask = deletedTasks.value.shift();
        tasks.value.push(recoveredTask);
      }
    };

    const completeTask = (index) => {
      tasks.value[index].completed = !tasks.value[index].completed;
    };

    const truncateText = (text, length) => {
      if (text.length > length) {
        return text.substring(0, length) + '...';
      }
      return text;
    };

    const updateNewTask = (event) => {
      newTask.value = event.target.value;
    };

    return {
      tasks,
      addTask,
      deletedTasks,
      recoverTask,
      truncateText,
      completeTask,
      deleteTask,
      updateNewTask,
    };
  },
};
</script>
