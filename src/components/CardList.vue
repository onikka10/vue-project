<script setup>
import Card from './Card.vue';

const onClickAdd = () => {
    
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card 
    title="Мужские Кроссовки Nike Blazer Mid Suede" 
    :price="5000" 
    imgageUrl="/sneakers/sneakers-1.jpg"
    :isFavorite="false"
    :onClickFavorite="onClickAdd"
    :isAdded="false"
    :onClickAdd="onClickAdd"
    />


    <Card title="Мужские Кросовки " :price="5000" imgageUrl="/sneakers/sneakers-2.jpg"/>
    <Card title="" :price="5000" imgageUrl="/sneakers/sneakers-3.jpg"/>
    <Card title="" :price="5000" imgageUrl="/sneakers/sneakers-4.jpg"/>
  </div>
</template>
