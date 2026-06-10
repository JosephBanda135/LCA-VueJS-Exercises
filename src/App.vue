<script setup>
import { ref } from "vue";
import TicketCard from "./components/TicketCard.vue";

const tickets = ref([
  {
    id: 1,
    name: "Bronze",
    price: 199,
    description: "Perfect for first-time visitors.",
    benefits: ["Entry", "Food stalls"],
    featured: false,
    favourite: false,
  },
  {
    id: 2,
    name: "Silver",
    price: 399,
    description: "More food and fun.",
    benefits: ["Entry", "Food stalls", "Music zone"],
    featured: false,
    favourite: false,
  },
  {
    id: 3,
    name: "Gold",
    price: 699,
    description: "Full VIP experience.",
    benefits: ["Entry", "Food stalls", "Music", "VIP lounge"],
    featured: true,
    favourite: false,
  },
]);

function toggleFavourite(ticket) {
  ticket.favourite = !ticket.favourite;
}
</script>

<template>
  <div class="page">
    <h1>Cape Town Food Fest</h1>
    <p>Food, music and unforgettable experiences.</p>
    <div class="grid">
      <div v-for="ticket in tickets" :key="ticket.id">
        <TicketCard :ticket="ticket" />

        <button @click="toggleFavourite(ticket)">
          {{ ticket.favourite ? "❤️ Favourited" : "🤍 Favourite" }}
        </button>
      </div>
    </div>
  </div>
</template>

<style>
.page {
  text-align: center;
  font-family: Arial, sans-serif;
}
/*
.grid {
  display: flex;
  gap: 15px;
  justify-content: center;
  flex-wrap: wrap;
}
*/
.card-wrapper {
  width: 250px;
}

button {
  margin-top: 10px;
  padding: 8px;
  border: none;
  cursor: pointer;
  background: #333;
  color: white;
  border-radius: 5px;
}
.bronze {
  border: 2px solid #cd7f32;
}

.silver {
  border: 2px solid #c0c0c0;
}

.gold {
  border: 2px solid #d4af37;
}

.featured {
  background: #fff8dc;
  transform: scale(1.05);
}

.grid {
  display: flex;
  gap: 20px;
  justify-content: center;
  flex-wrap: wrap;
  margin-top: 20px;
}
</style>
