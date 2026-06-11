<script setup>
import { ref, computed } from "vue";
import PropertyCard from "./components/PropertyCard.vue";

import Seapoint from "./assets/Seapoint.jpg";
import campsbay from "./assets/camps bay.jpg";
import woodstock from "./assets/woodstock.jpg";

const properties = ref([
  {
    id: 1,
    title: "Sea Point Apartment",
    location: "Cape Town",
    price: 1200,
    type: "Apartment",
    image: Seapoint,
    available: true,
  },
  {
    id: 2,
    title: "Camps Bay Villa",
    location: "Cape Town",
    price: 3500,
    type: "Villa",
    image: campsbay,
    available: true,
  },
  {
    id: 3,
    title: "Woodstock Loft",
    location: "Cape Town",
    price: 1800,
    type: "Loft",
    image: woodstock,
    available: false,
  },
]);

const search = ref("");
const sortOrder = ref("default");

const filteredProperties = computed(() => {
  let result = properties.value.filter((property) => {
    return (
      property.title.toLowerCase().includes(search.value.toLowerCase()) ||
      property.location.toLowerCase().includes(search.value.toLowerCase())
    );
  });

  if (sortOrder.value === "lowToHigh") {
    result.sort((a, b) => a.price - b.price);
  }

  if (sortOrder.value === "highToLow") {
    result.sort((a, b) => b.price - a.price);
  }

  return result;
});
</script>

<template>
  <h1>Homes & Beyond</h1>
  <p>Total Properties:{{ filteredProperties.length }}</p>
  <div class="controls">
    <input v-model="search" placeholder="Search properties..." />

    <select v-model="sortOrder">
      <option value="default">Default</option>
      <option value="lowToHigh">Price: Low to High</option>
      <option value="highToLow">Price: High to Low</option>
    </select>
  </div>

  <div class="container">
    <PropertyCard
      v-for="property in filteredProperties"
      :key="property.id"
      :title="property.title"
      :location="property.location"
      :price="property.price"
      :type="property.type"
      :image="property.image"
      :available="property.available"
    />
  </div>
</template>

<style>
.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 20px;
  margin-top: 20px;
}

.controls {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin: 20px 0;
  flex-wrap: wrap;
}
</style>
