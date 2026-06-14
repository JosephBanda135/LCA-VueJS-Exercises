<script setup>
defineProps({
  name: String,
  price: Number,
  soldOut: Boolean,
});
</script>

<template>
  <div class="card">
    <h2>{{ name }}</h2>

    <p>R{{ price }}</p>

    <button v-if="!soldOut" @click="$emit('add-to-cart')">Add to Cart</button>

    <button v-else disabled>Sold Out</button>
  </div>
</template>

<style>
.card {
  width: 250px;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 10px;
  background: white;
  text-align: center;
  margin: 10px;
  transition: 0.2s ease;
}

.card:hover {
  transform: translateY(-3px);
}

h2 {
  color: #2c3e50;
}

button {
  margin-top: 10px;
  padding: 6px 10px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  background: #42b983;
  color: white;
}

button:disabled {
  background: #ccc;
  cursor: not-allowed;
}
</style>
