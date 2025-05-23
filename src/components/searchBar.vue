<script setup>
import { ref, watch } from "vue";

const searchText = ref("");
const allItems = ref(["Manzana", "Banana", "Naranja", "Fresa", "Mango",
    "Uva", "Piña", "Sandía", "Melón", "Pera",
    "Kiwi", "Frambuesa", "Arándano", "Mora", "Cereza",
    "Melocotón", "Albaricoque", "Ciruela", "Higo", "Granada",
    "Lima", "Limón", "Aguacate", "Coco", "Papaya",
    "Guayaba", "Maracuyá", "Níspero", "Caqui", "Lichi",
    "Grosella", "Zarzamora", "Madroño", "Membrillo", "Tamarindo",
    "Carambola", "Pitahaya", "Feijoa", "Mangostán", "Rambután",
    "Chirimoya", "Zapote", "Jaca", "Durazno", "Nectarina",
    "Pomelo", "Mandarina", "Toronja", "Plátano", "Higo chumbo"]);
const searchResults = ref([]);

watch(searchText, (newText) => {
  if (newText) {
    searchResults.value = allItems.value.filter((item) =>
      item.toLowerCase().includes(newText.toLowerCase())
    );
  } else {
    searchResults.value = [];
  }
});

</script>

<template>
  <div
    class="m-10 w-lg py-2 px-3 select-none"
  >
    <input
      type="text"
      name="search"
      v-model="searchText"
      class="shadow shadow-gray-500 appearance-none border bg-gray-200 rounded-3xl w-full py-2 px-10 text-gray-800 leading-tight focus:shadow-outline focus:outline-2 focus:outline-offset focus:outline-blue-600"
      placeholder="Buscar..."
    />
    <svg class="absolute translate-x-3 -translate-y-7.5 fill-gray-500" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M19.023 16.977a35.13 35.13 0 0 1-1.367-1.384c-.372-.378-.596-.653-.596-.653l-2.8-1.337A6.962 6.962 0 0 0 16 9c0-3.859-3.14-7-7-7S2 5.141 2 9s3.14 7 7 7c1.763 0 3.37-.66 4.603-1.739l1.337 2.8s.275.224.653.596c.387.363.896.854 1.384 1.367l1.358 1.392.604.646 2.121-2.121-.646-.604c-.379-.372-.885-.866-1.391-1.36zM9 14c-2.757 0-5-2.243-5-5s2.243-5 5-5 5 2.243 5 5-2.243 5-5 5z">
    </path></svg>
    <button
      v-if="searchText"
      type="button"
      class="absolute -translate-x-10 translate-y-1.5 focus:outline-none"
      @click="searchText = ''"
    >
      <svg class="rounded-4xl bg-gray-300" xmlns="http://www.w3.org/2000/svg" width="26" height="26" viewBox="0 0 24 24"><path d="m16.192 6.344-4.243 4.242-4.242-4.242-1.414 1.414L10.535 12l-4.242 4.242 1.414 1.414 4.242-4.242 4.243 4.242 1.414-1.414L13.364 12l4.242-4.242z"></path></svg>
    </button>
    <ul
      v-if="searchResults.length > 0"
      class="overflow-auto max-h-96 border bg-white rounded-lg shadow-md mt-1.5"
    >
      <li
        v-for="result in searchResults"
        :key="result"
        class="aum text-pretty py-2 px-4 rounded-lg hover:bg-gray-100 hover:font-medium"
      >
        {{ result }}
      </li>
    </ul>
    <p
      v-else-if="searchText && searchResults.length === 0"
      class="text-gray-500 mt-2"
    >
      No se encontraron resultados para "{{ searchText }}".
    </p>
  </div>
</template>

<style scoped>
.aum:hover {
  font-size: 1.4rem;
  transition: font-size 0.3s ease-in-out;
}
</style>
