// components/CategoryCard.vue
<template>
  <div class="card">
    <div class="placeholder" v-if="showPlaceholder">{{ placeholderText }}</div>
    <div class="card-image" v-if="imageUrl">
      <img :src="imageUrl" alt="Card Image" />
    </div>
    <div class="card-content">
      <h2 v-if="title">{{ title }}</h2>
      <slot name="content"></slot>
      <div v-if="categories.length > 0">
        <div v-for="category in categories" :key="category" class="rating-section">
          <h3>{{ category }}</h3>
          <StarRating :category="category" @update-rating="updateRating" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import StarRating from './StarRating.vue';

export default {
  props: {
    title: {
      type: String,
      default: '',
    },
    categories: {
      type: Array,
      default: () => [],
    },
    placeholderText: {
      type: String,
      default: 'Placeholder',
    },
    showPlaceholder: {
      type: Boolean,
      default: true,
    },
    imageUrl: {
      type: String,
      default: '',
    },
  },
  components: { StarRating },
  methods: {
    updateRating(category, rating) {
      this.$emit('update-rating', category, rating);
    },
  },
};
</script>

<style scoped>
.card {
  display: inline-block;
  width: 20vw;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  text-align: center;
  background-color: white;
  margin-bottom: 20px;
}
.placeholder {
  height: 150px;
  background-color: #f0f0f0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 18px;
  color: #aaa;
  margin-bottom: 20px;
}
.card-image img {
  width: 100%;
  height: auto;
  border-bottom: 1px solid #ddd;
}

.rating-section h3 {
  margin-bottom: 0px;
}
</style>
