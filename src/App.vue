<template>
  <div class="app-container">
    <div class="background-image">
      <img src="./assets/bg-cafe-lg.jpg" alt="Coffee shop background" class="desktop-bg" />
      <img src="./assets/bg-cafe.jpg" alt="Coffee shop background" class="mobile-bg" />
    </div>

    <main class="content">
      <div class="header">
        <h1>Our Collection</h1>
        <p>
          Introducing our Coffee Collection, a selection of unique coffees from different roast
          types and origins, expertly roasted in small batches and shipped fresh weekly.
        </p>
      </div>

      <div class="controls">
        <button
          v-for="tab in tabs"
          :key="tab"
          :class="{ active: activeTab === tab }"
          @click="activeTab = tab"
        >
          {{ tab }}
        </button>
      </div>
      <div class="products">
        <CoffeeCard v-for="coffee in filteredCoffees" :key="coffee.id" :coffee="coffee" />
      </div>
    </main>
    <footer class="footer">
      <p>created by <a href="https://github.com/may4eto">may4eto</a> - devChallenges.io</p>
    </footer>
  </div>
</template>

<script>
import CoffeeCard from './components/CoffeeCard.vue'

export default {
  components: { CoffeeCard },
  data() {
    return {
      activeTab: 'All Products',
      tabs: ['All Products', 'Available Now'],
      coffees: [
        {
          id: 1,
          name: 'Cappuccino',
          url: 'images/cappuccino.jpg',
          price: 8.2,
          rating: 4.7,
          votes: 65,
          available: true,
          popular: true
        },
        {
          id: 2,
          name: 'House Coffee',
          url: 'images/house-coffee.jpg',
          price: 8.0,
          rating: 4.85,
          votes: 14,
          available: true,
          popular: true
        },
        {
          id: 3,
          name: 'Espresso',
          url: 'images/espresso.jpg',
          price: 2.5,
          rating: 4.9,
          votes: 55,
          available: true,
          popular: true
        },
        {
          id: 4,
          name: 'Coffee Latte',
          url: 'images/coffee-latte.jpg',
          price: 4.5,
          rating: 5.0,
          votes: 23,
          available: true,
          popular: false
        },
        {
          id: 5,
          name: 'Chocolate Coffee',
          url: 'images/chocolate-coffee.jpg',
          price: 4.0,
          rating: 4.65,
          votes: 122,
          available: false,
          popular: false
        },
        {
          id: 6,
          name: 'Valentine Special',
          url: 'images/valentine-special.jpg',
          price: 5.5,
          rating: null,
          votes: 0,
          available: true,
          popular: false
        }
      ]
    }
  },
  computed: {
    filteredCoffees() {
      if (this.activeTab === 'Available Now') {
        return this.coffees.filter((coffee) => coffee.available)
      }
      return this.coffees
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'DM Sans', sans-serif;
}

.app-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  position: relative;
  padding: 2rem;
  background-color: #000;
}

.background-image {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.background-image img {
  width: 100%;
  object-fit: contain;
}

.desktop-bg {
  display: block;
}

.mobile-bg {
  display: none;
}

.content {
  background-color: #1b1d1f;
  font-size: 1.25rem;
  border-radius: 12px;
  padding: 2rem;
  max-width: 1200px;
  width: 100%;
  margin: 2rem;
  z-index: 1;
}

.header {
  text-align: center;
  margin-bottom: 2rem;
  color: #fef7ee;
  background-image: url('images/vector.svg');
  background-position: center;
  background-size: contain;
}

.header h1 {
  font-size: 2rem;
  margin-bottom: 1rem;
}

.header p {
  color: #6f757c;
  max-width: 600px;
  margin: 0 auto;
}

.footer {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
}

.footer p,
.footer a {
  color: #6f757c;
}

.controls {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 2rem;
}

.controls button {
  background: none;
  border: none;
  color: #fef7ee;
  padding: 0.5rem 1rem;
  border-radius: 8px;
  cursor: pointer;
  font-weight: 600;
}

.controls button.active {
  background-color: #6f757c;
}

.products {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1.5rem;
}

@media (max-width: 768px) {
  .desktop-bg {
    display: none;
  }

  .mobile-bg {
    display: block;
  }

  .content {
    padding: 1rem;
  }

  .products {
    grid-template-columns: 1fr;
  }
}
</style>
