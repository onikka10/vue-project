<script setup>
import Header from './components/Header.vue';
import axios from 'axios';
import CardList from './components/CardList.vue'; 
import Drawer from './components/Drawer.vue';
import { onMounted, provide, reactive, ref, watch} from 'vue';


const items = ref([]);
const cart = ref([]);

const drawwerVisible = ref(false);

const closeDrawer = () => {
  drawwerVisible.value = false;
}
const openDrawer = () => {
  drawwerVisible.value = true;
}
const filters = reactive({
  sortBy: 'title',
  searchQuery: ''
});


const addToCart = (item)=> {
  cart.value.push(item);
    item.isAdded = true 
}

const removeFromCart = (item) => {
  cart.value.splice(cart.value.indexOf(item), 1);
  item.isAdded = false
}


const addToFromPlus = (item) => {
  if (!item.isAdded) {
    addToCart(item);
  } else { 
    removeFromCart(item);
  }
  console.log(cart);
  
} 
 

const onChangeSelect= (event) => {
  filters.sortBy = event.target.value
}

const onChangeSearchInput = (event) => {
  filters.searchQuery = event.target.value
}


const fetchFavorites = async () => {
  try {
    const { data:favorites } = await axios.get(`https://8c35c1a1a654cf55.mokky.dev/favorites`);


items.value = items.value.map(item => {
  const favorite = favorites.find(favorite => favorite.parentid === item.id);

 if (!favorite) {
   return item;
  } 

  return {
    ...item,
    isFavorite: true,
    favoriteId: favorite.id,
  }
})
  } catch (err) {
    console.log(err)
  }
}

const addToFavorite = async (item) => {
  try {
    if (!item.isFavorite) {
      const obj = {
        parentid: item.id,
      }
      item.isFavorite = !item.isFavorite
      const { data } = await axios.post(`https://8c35c1a1a654cf55.mokky.dev/favorites`, obj);

      
      item.favoriteId = data.id;
      console.log(data)

    } else { 
      item.isFavorite = !item.isFavorite
      item.favoriteId = null
      await axios.delete(`https://8c35c1a1a654cf55.mokky.dev/favorites/${item.favoriteId}`);
      
      
    }
  }catch (err) {
    console.log(err)
  }
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

  

    items.value = data.map((obj)=> ({
      ...obj,
      isFavorite: false,
      favoriteId: null,
      isAdded:false
    }));


  } catch (error) {
    console.log(error)
  }
}

onMounted(async () => {
  await fetchItems();
 await fetchFavorites();
});
watch(filters, fetchItems);

provide('cart', {
  cart,
  closeDrawer,
  openDrawer,
  removeFromCart,
});
</script>

<template>
  <Drawer v-if="drawwerVisible" />
  <div class="bg-white w-4/5 m-auto h-auto rounded-xl shadow-xl mt-14 ">
    <Header @open-drawer="openDrawer" />

    
    
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

        <div class="mt-10">
          <CardList :items="items" @add-to-favorite="addToFavorite" @add-to-cart="addToFromPlus"/>
        </div>
    </div>
    
</div>
</template>
