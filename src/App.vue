<template>
  <div class="app">
    <h1>Rate Artworks</h1>
    <div class="card-separator">
    <div v-for="(card, index) in cards" :key="index" class="category-card">
      <CategoryCard :categories="categories" :title="card.title" @update-rating="updateRating" />
    </div>
    </div>
    <button @click="submitRatings">Submit</button>
  </div>
</template>

<script>
import CategoryCard from './components/CategoryCard.vue';

export default {
  components: { CategoryCard },
  data() {
    return {
      categories: ['Fits to my Wall', 'Thats my Style', 'Enjoy this Artist'],
      cards: [
        { title: 'Artwork 1' },
        { title: 'Artwork 2' },
        { title: 'Artwork 3' },
        { title: 'Artwork 4' },
      ],
      ratings: {},
    };
  },
  methods: {
    updateRating(category, rating) {
      if (!this.ratings[category]) {
        this.$set(this.ratings, category, {});
      }
      this.ratings[category][rating.title] = rating;
    },
    submitRatings() {
      console.log('Ratings:', this.ratings);
    },
  },
};
</script>

<style>
.app {
  font-family: Arial, sans-serif;
  text-align: center;
}
button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  border: none;
  border-radius: 4px;
  background-color: #582c82;
  color: white;
}
button:hover {
  background-color: #470d7e;
}
.category-card{
  margin-right: 1rem;
}
</style>
