<script setup>
import MyHello from './components/MyHello.vue';
</script>

<template>
<MyHello title="Кроссовки Nike"  :price="15000" is-added/>
<MyHello  is-Added/>
<MyHello :is-Added="false"/>
<MyHello />
<MyHello />
</template>

<style scoped>

</style>
