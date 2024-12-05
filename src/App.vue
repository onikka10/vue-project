<script setup>
import Header from './components/Header.vue';
import axios from 'axios';
import CardList from './components/CardList.vue'; 
import Drawer from './components/Drawer.vue';
import { onMounted, reactive, ref, watch} from 'vue';


const items = ref([]);

const filters = reactive({
  sortBy: 'title',
  searchQuery: ''
});



const onChangeSelect= (event) => {
  filters.sortBy = event.target.value
}

const onChangeSearchInput = (event) => {
  filters.searchQuery = event.target.value
}


const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy

    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`;
        
      }


    const { data } = await axios.get(`https://8c35c1a1a654cf55.mokky.dev/items`, {
      params
    });
    items.value = data
  } catch (error) {
    console.log(error)
  }
}

onMounted(fetchItems);
watch(filters, fetchItems);
</script>

<template>
  <!-- <Drawer /> -->
  <div class="bg-white w-4/5 m-auto h-auto rounded-xl shadow-xl mt-14 ">
    <Header />

    
    
    <div class="p-10">
        <div class="flex justify-between items-center">
      <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>

         <div class="flex gap-4">

          <select @change="onChangeSelect" class="py-2 px-3 border rounded-md outline-none items-center" name="" id="">
            <option value="name">По названию</option>
            <option value="price">По цене (дешевые)</option>
            <option value="-price">По цене (дорогие)</option>
          </select>

          <div class="relative w-full md:w-auto">
              <img
              class="absolute left-4 top-1/2 transform -translate-y-1/2"
              src="/search.svg"/>

              <input @input="onChangeSearchInput" class="border rounded-md py-2 pl-11 pr-4 w-full md:w-64 outline-none focus:border-gray-400" type="text" placeholder="Поиск..."/>
            </div>
          </div>
        </div>

        <div class="mt-10"><CardList :items="items" /></div>
    </div>
    
</div>
</template>
