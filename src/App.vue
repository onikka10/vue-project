<script setup>
import MyHello from './components/MyHello.vue';
</script>

<template>
<MyHello title="Кроссовки Nike"  :price="15000" is-added>
    <button>Добавить</button>
</MyHello>
<MyHello  is-Added/>
<MyHello :is-Added="false">
    <h4>123123</h4>
</MyHello>
<MyHello>
    <MyHello />
    </MyHello>

</template>

<style scoped>

</style>
