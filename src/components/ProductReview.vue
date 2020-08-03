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
      Would you recommend this product?
      <input id="yes" name="recommend" type="radio" value="Yes, I'd recommend" v-model="recommend"><label for="yes">Yes</label>
      <input id="no" name="recommend" type="radio" value="No, I wouldn't recommend" v-model="recommend"><label for="no">No</label>
    </p>
    <p>
      <input type="submit" value="Submit"/>
    </p>
  </form>
</template>

<script>
  import {eventBus} from "../main";

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

          eventBus.$emit('review-submitted', productReview);
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
  .review-form {
    width: 400px;
    padding: 20px;
    margin: 40px;
    border: 1px solid #d8d8d8;
  }

  input {
    width: 100%;
    height: 25px;
    margin-bottom: 20px;
  }

  textarea {
    width: 100%;
    height: 60px;
  }
</style>
