<script setup>
import { ref, watch } from "vue";

const searchText = ref("");
const isFocused = ref(false);

//* array, donde busca los resultados
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

//* Observa si sucedio algun cambio en el input
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

  
  <!-- * Contenedor input -->
  <div class="w-lg relative m-auto mt-10 select-none">

    <!-- * input -->
    <input
    type="text"
      name="search"
      v-model="searchText"
      @focus="isFocused = true"
      @blur="isFocused = false"
      class="relative shadow shadow-gray-500 appearance-none border bg-gray-200 rounded-3xl w-full py-2 px-10 text-gray-800 leading-tight focus:outline-blue-500 transition-all duration-500"
      placeholder="Buscar..."
    />

    <!-- * img lupa -->
    <svg class="absolute translate-x-3 -translate-y-7.5 fill-gray-500" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M19.023 16.977a35.13 35.13 0 0 1-1.367-1.384c-.372-.378-.596-.653-.596-.653l-2.8-1.337A6.962 6.962 0 0 0 16 9c0-3.859-3.14-7-7-7S2 5.141 2 9s3.14 7 7 7c1.763 0 3.37-.66 4.603-1.739l1.337 2.8s.275.224.653.596c.387.363.896.854 1.384 1.367l1.358 1.392.604.646 2.121-2.121-.646-.604c-.379-.372-.885-.866-1.391-1.36zM9 14c-2.757 0-5-2.243-5-5s2.243-5 5-5 5 2.243 5 5-2.243 5-5 5z">
    </path></svg>

    <!-- * Borrador (X) -->
    <button
      v-if="searchText"
      type="button"
      class="absolute -translate-x-10 translate-y-1.5 focus:outline-none"
      @click="searchText = ''"
    >
      <svg class="rounded-4xl bg-gray-300" xmlns="http://www.w3.org/2000/svg" width="26" height="26" viewBox="0 0 24 24"><path d="m16.192 6.344-4.243 4.242-4.242-4.242-1.414 1.414L10.535 12l-4.242 4.242 1.414 1.414 4.242-4.242 4.243 4.242 1.414-1.414L13.364 12l4.242-4.242z">
      </path></svg>
    </button>
    
    
  </div>

  <!-- * Notificaciones -->
  <div class="absolute">
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M12 22a2.98 2.98 0 0 0 2.818-2H9.182A2.98 2.98 0 0 0 12 22zm7-7.414V10c0-3.217-2.185-5.927-5.145-6.742C13.562 2.52 12.846 2 12 2s-1.562.52-1.855 1.258C7.185 4.074 5 6.783 5 10v4.586l-1.707 1.707A.996.996 0 0 0 3 17v1a1 1 0 0 0 1 1h16a1 1 0 0 0 1-1v-1a.996.996 0 0 0-.293-.707L19 14.586z">
    </path></svg>
  </div>

  <div class="relative w-lg m-auto mt-2 select-none">
    <!-- * Resultado en lista -->
    <ul
      v-if="searchResults.length > 0"
      class="overflow-auto absolute z-50 max-h-96 border bg-gray-200 rounded-lg shadow-md mt-1.5 w-full"
    >
      <li
        v-for="result in searchResults"
        :key="result"
        class="aum text-pretty py-2 px-4 rounded-lg hover:bg-gray-300 hover:font-medium transition-all duration-300"
      >
        {{ result }}
      </li>
    </ul>

    <!-- * no encontro ningun resultado -->
    <p
      v-else-if="searchText && searchResults.length === 0"
      class="absolute z-50 text-gray-600 mt-2 w-full rounded-lg bg-gray-100 text-center"
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
