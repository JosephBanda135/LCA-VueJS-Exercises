<script setup>
defineProps({
  ticket: Object,
});
</script>

<template>
  <div
    class="card"
    :class="[{ featured: ticket.featured }, ticket.name.toLowerCase()]"
  >
    <h2>
      {{ ticket.name }}
      <span v-if="ticket.favourite">❤️</span>
    </h2>

    <p>R{{ ticket.price }}</p>
    <p>{{ ticket.description }}</p>

    <ul>
      <li v-for="b in ticket.benefits" :key="b">
        {{ b }}
      </li>
    </ul>
  </div>
</template>

<style>
.featured {
  border: 2px solid gold;
  background: #fff8dc;
}

ul {
  padding-left: 15px;
}

.card {
  width: 280px;
  padding: 20px;
  border-radius: 12px;
  background: white;
  margin: 10px auto;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s ease;
}

.card:hover {
  transform: scale(1.03);

  .bronze {
    border: 2px solid #cd7f32;
  }

  .silver {
    border: 2px solid #c0c0c0;
  }

  .gold {
    border: 2px solid #d4af37;
  }
}

.featured {
  background: #fff8dc;
  transform: scale(1.05);
}
</style>
