<script setup>
import { ref, watch } from "vue";

const searchText = ref("");
const allItems = ref(["Manzana", "Banana", "Naranja", "Mandarina", "Kiwi"]);
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
    class="m-10 bg-gray-200 appearance-none border w-lg rounded-lg py-2 px-3"
  >
    <input
      type="text"
      v-model="searchText"
      class="shadow shadow-gray-500 appearance-none border bg-white rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
      placeholder="Buscar..."
    />
    <button
      v-if="searchText"
      type="button"
      class="absolute -translate-x-10 translate-y-1.5 focus:outline-none"
      @click="searchText = ''"
    >
      <span>❌</span>
    </button>
    <ul
      v-if="searchResults.length > 0"
      class="border bg-white rounded shadow-md mt-1.5"
    >
      <li
        v-for="result in searchResults"
        :key="result"
        class="aum py-2 px-4 rounded hover:bg-gray-100 hover:font-medium"
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
