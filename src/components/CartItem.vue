<script setup>
defineProps({
  img: String,
  title: String,
  price: Number,
  onClickDelete: Function,
});
</script>

<template>

<div class="flex items-center border border-slate-200 p-4 rounded-xl gap-4">
  <img class="w-16 h-16" src="/sneakers/sneakers-1.jpg" alt="Sneakers" />

  <div class="flex flex-col w-full">
    <p>Мужские кросовки</p>
    
    <div class="flex justify-between mt-2">
      <b>12990 rb</b>
      <img class="opacity-40 hover:opacity-100 cursor-pointer transition" src="/close.svg" alt="delete" />  
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
