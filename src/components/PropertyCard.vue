<script setup>
defineProps({
  title: String,
  location: String,
  price: Number,
  type: String,
  image: String,
  available: Boolean,
});
</script>

<template>
  <div class="card">
    <img :src="image" :alt="title" />
    <h2>{{ title }}</h2>

    <p>{{ location }}</p>
    <p>R{{ price }}</p>
    <p>{{ type }}</p>
    <p v-if="!available" class="badge">Not Available</p>
  </div>
</template>

<style>
.card {
  width: 280px;
  padding: 15px;
  border-radius: 12px;
  background: white;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  transition: transform 0.3s ease;
}

.card:hover {
  transform: translateY(-5px);
}

img {
  width: 100%;
  height: 180px;
  object-fit: cover;
  border-radius: 10px;
}

.badge {
  background-color: #ff4d4d;
  color: white;
  padding: 5px 10px;
  border-radius: 6px;
  display: inline-block;
  margin-top: 8px;
  font-size: 12px;
}
</style>
