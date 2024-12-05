<script setup>
const emit= defineEmits(['onClickRemove']);

defineProps({
  id: Number,
  imageUrl: String,
  title: String,
  price: Number,
});
</script>

<template>

<div class="flex items-center border border-slate-200 p-4 rounded-xl gap-4">
  <img class="w-16 h-16" :src="imageUrl" :alt="title" />

  <div class="flex flex-col w-full flex-1">
    <p>{{title}}</p>
    
    <div class="flex justify-between mt-2 ">
      <b class="flex-1">{{price}} руб</b>
      <img @click="emit('onClickRemove')" class="opacity-40 hover:opacity-100 cursor-pointer transition" src="/close.svg" />
  
    </div>
  </div>
</div>


  <!-- <div class="relative flex w-full border border-slate-100 rounded-xl p-4 gap-4">
    <img :src="img" class="w-16 h-16" alt="Sneaker" />
    <div class="flex flex-col w-full">
      <p>{{ title }}</p>
      <div class="flex justify-between mt-5">
        <span class="font-bold">{{ price }} руб.</span>
        <img
          class="cursor-pointer opacity-30 hover:opacity-100 transition"
          src="/close.svg"
          alt="Close"
        />
      </div>
    </div>
  </div> -->


  
</template>
