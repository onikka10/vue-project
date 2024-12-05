<script setup>
import { inject } from 'vue';
import Card from './Card.vue';

defineProps({
  items: Array,
})


const onClickFavorite = inject('addToFavorite');

</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card 
  v-for="item in items"
  :key="item.id"
  :id="item.id"
  :title="item.title"
  :price="item.price"
  :imgageUrl="item.imageUrl"
  :onClickFavorite="() => onClickFavorite(item)" 
  :isFavorite="item.isFavorite"
    />
  </div>
</template>
