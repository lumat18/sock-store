<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <p v-if="errors.length">
      <b>Please correct the following error(s):</b>
    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>
    </p>
    <p>
      <label for="name">Name:</label>
      <input id="name" v-model="name" type="text">
    </p>
    <p>
      <label for="review">Review:</label>
      <textarea id="review" v-model="review"></textarea>
    </p>
    <p>
      <label for="rating">Rating:</label>
      <select id="rating" v-model.number="rating">
        <option>5</option>
        <option>4</option>
        <option>3</option>
        <option>2</option>
        <option>1</option>
      </select>
    </p>
    <p>
      Would you recommend this product?<br/>
      <input id="yes" name="recommend" type="radio" value="Yes, I'd recommend" v-model="recommend"><label for="yes">Yes</label> <br/>
      <input id="no" name="recommend" type="radio" value="No, I wouldn't recommend" v-model="recommend"><label for="no">No</label>
    </p>
    <p>
      <input type="submit" value="Submit"/>
    </p>
  </form>
</template>

<script>
  export default {
    data() {
      return {
        name: null,
        review: null,
        rating: null,
        errors: [],
        recommend: null
      }
    },
    methods: {
      onSubmit() {
        this.errors = [];
        if (this.name && this.review && this.rating) {
          let productReview = {
            name: this.name,
            review: this.review,
            rating: this.rating,
            recommend: this.recommend
          }
          this.name = null;
          this.review = null;
          this.rating = null;
          this.recommend = null;

          this.$emit('review-submitted', productReview);
        } else {
          if (!this.name) this.errors.push('Name required');
          if (!this.review) this.errors.push('Review required');
          if (!this.rating) this.errors.push('Rating required');
        }

      }
    }
  }
</script>

<style scoped>

</style>
