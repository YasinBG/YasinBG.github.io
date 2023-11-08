<template>
  <div>

<input class="w-60 h-12 border-2 border-green-500 rounded mx-auto font-semibold"/>

<ul class="flex flex-col my-6">
    <li class="flex text-start my-2 font-semibold">
        <input type="text">
        <span></span>
        <div>
            <button class="border-red-800 border-2 text-center uppercase rounded bg-red-400 text-white w-12 h-6 font-semibold">sil</button>
        </div>
    </li>
</ul>

<button class=" font-semibold border-2 border-green-600 text-center uppercase rounded bg-green-400 text-white hover:bg-green-600">geri al</button>
</div>
</template>

<script>



export default {
  name: 'HomeView',
  components: {
    
  }
}
</script>
