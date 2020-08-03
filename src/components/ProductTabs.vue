<template>
  <div>
    <div>
      <span class="tab"
            :class="{activeTab: selectedTab === tab}"
            v-for="(tab, index) in tabs"
            :key="index"
            @click="selectedTab=tab">{{ tab }}</span>
    </div>
    <div v-if="selectedTab === 'Reviews'">
      <h2>Reviews</h2>
      <p v-if="reviews.length === 0">There are no reviews yet</p>
      <ul>
        <li v-for="review in reviews">
          <p>{{ review.name }}</p>
          <p>{{ review.review }}</p>
          <p>{{ review.rating }}</p>
          <p>{{ review.recommend }}</p>
        </li>
      </ul>
    </div>
    <div v-show="selectedTab === 'Make a review'">
      <ProductReview />
    </div>
  </div>


</template>

<script>
  import ProductReview from "./ProductReview";

  export default {
    components: {ProductReview},
    props: {
      reviews: {
        type: Array,
        required: true
      }
    },
    data() {
      return {
        tabs: ['Reviews', 'Make a review'],
        selectedTab: 'Reviews'
      }
    }
  }
</script>

<style scoped>
  .tab {
    margin-left: 20px;
    cursor: pointer;
  }

  .activeTab {
    color: #16C0B0;
    text-decoration: underline;
  }
</style>
