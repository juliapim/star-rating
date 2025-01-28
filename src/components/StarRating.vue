<template>
  <div class="star-rating">
    <div class="stars">
      <span
        v-for="n in 5"
        :key="n"
        class="star"
        :class="{ filled: n <= rating, hover: n <= hoverRating }"
        @click="setRating(n)"
        @mouseover="hoverRating = n"
        @mouseleave="hoverRating = 0"
      >
      &#9733;
      </span>
    </div>
    <p style="margin-top: 0px">{{ hoverRating > 0 ? hoverRating : rating }}/5</p>  </div>
</template>

<script>
export default {
  props: {
    category: String,
  },
  data() {
    return {
      rating: 0,
      hoverRating: 0,
    };
  },
  methods: {
    setRating(value) {
      this.rating = value;
      this.$emit('update-rating', value);
    },
  },
};
</script>

<style scoped>
.star-rating {
  display: inline-block;
  text-align: center;
  margin-top: 10px;
}
.stars {
  display: inline-flex;
  gap: 5px;
  cursor: pointer;
  
}
.star {
  font-size: 15px;
  transition: color 0.2s;
  color: #ddd;
}
.star.filled {
  color: #ffc107;
}
.star.hover {
  color: #ffdd44;
}
</style>
