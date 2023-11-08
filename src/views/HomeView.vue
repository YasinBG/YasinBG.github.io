<template>
  <div class="bg-cover h-screen flex justify-center items-center mt-6" style="background-image: url('https://cdn.pixabay.com/photo/2017/05/09/13/33/laptop-2298286_1280.png'); background-position: center;">
    <div class="w-4/5 md:w-3/5 lg:w-1/3">
      <h2 class="text-3xl text-green-300 text-center my-8">Todo-List Uygulaması</h2>
      <input
        class="w-full h-12 border-2 border-green-500 rounded mx-auto font-semibold mb-4"
        :value="newTask"
        @input="updateNewTask"
        @keyup.enter="addTask"
        placeholder=" Görev Ekle..."
        style="position: sticky; top: 0; background-color: white;"
      />
      <div class="mx-auto">
        <ul class="flex justify-center flex-col my-2" v-for="(task, index) in tasks" :key="index">
          <li class="flex justify-center mx-auto font-semibold my-2">
            <input class="mr-2 md:mr-4 w-6 h-6 self-center" type="checkbox" @change="completeTask(index)" :checked="task.completed" />
            <span class="mx-2 md:mx-4" :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">
              {{ truncateText(task.baslik, 20) }}
            </span>
            <div class="ml-2 md:ml-4">
              <button
                @click="deleteTask(index)"
                class="border-red-800 border-2 text-center uppercase rounded text-white font-semibold"
              >
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="text-red-600 w-6 h-6">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
                </svg>
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
