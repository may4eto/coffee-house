<template>
  <div class="coffee-card" :class="{ 'sold-out': !coffee.available }">
    <div class="coffee-image">
      <img :src="coffee.url" :alt="coffee.name" />
      <span v-if="coffee.popular" class="popular-badge">Popular</span>
    </div>

    <div class="coffee-info">
      <div class="name-price">
        <h3>{{ coffee.name }}</h3>
        <span class="price">${{ coffee.price.toFixed(2) }}</span>
      </div>

      <div class="rating">
        <div class="stars">
          <img
            v-for="i in 5"
            :key="i"
            :src="i <= Math.round(coffee.rating) ? starFilled : starEmpty"
            alt="star"
          />
        </div>
        <div v-if="coffee.rating !== null" class="votes">
          ({{ coffee.rating }}/5 <span class="vote-count">{{ coffee.votes }} votes</span>)
        </div>
        <div v-else class="no-rating">No ratings</div>
      </div>

      <div v-if="!coffee.available" class="sold-out-badge">Sold out</div>
    </div>
  </div>
</template>

<script>
import starFilled from '../assets/Star_fill.svg'
import starEmpty from '../assets/Star.svg'

export default {
  props: {
    coffee: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      starFilled,
      starEmpty
    }
  }
}
</script>

<style scoped>
.coffee-card {
  background-color: #1b1d1f;
  border-radius: 12px;
  padding: 1rem;
  position: relative;
  transition: transform 0.3s ease;
}

.coffee-card:hover {
  transform: translateY(-5px);
}

.coffee-card.sold-out {
  opacity: 0.6;
}

.coffee-image {
  position: relative;
  margin-bottom: 1rem;
}

.coffee-image img {
  width: 100%;
  height: 150px;
  object-fit: cover;
  border-radius: 12px;
}

.popular-badge {
  position: absolute;
  top: 0.5rem;
  left: 0.5rem;
  background-color: #f6c768;
  color: #111315;
  padding: 0.25rem 0.5rem;
  border-radius: 1rem;
  font-size: 0.75rem;
  font-weight: 600;
}

.name-price {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.5rem;
}

.name-price h3 {
  color: #fef7ee;
  font-size: 1rem;
}

.price {
  background-color: #bee3cc;
  color: #111315;
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
  font-weight: 600;
  font-size: 0.875rem;
}

.rating {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.stars {
  display: flex;
  gap: 0.25rem;
}

.stars img {
  width: 16px;
  height: 16px;
}

.votes,
.no-rating {
  color: #6f757c;
  font-size: 0.875rem;
}

.vote-count {
  color: #6f757c;
}

.sold-out-badge {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #ed735d;
  color: #111315;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  font-weight: 600;
  font-size: 0.875rem;
}
</style>
