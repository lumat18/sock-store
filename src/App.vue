<template>
  <div>
    <div class="nav-bar"></div>
    <div class="cart">
      <p>Cart({{ cart }})</p>
    </div>
    <product v-on:add-to-cart="addToCart"
             v-on:remove-from-cart="removeFromCart"
            :cart="cart"/>
  </div>
</template>

<script>
  import Product from "./components/Product";

  export default {
    components: {
      Product
    },
    data() {
      return {
        cart: 0
      }
    },
    methods: {
      addToCart: function () {
        this.cart += 1;
      },
      removeFromCart: function () {
        this.cart -= 1;
      }
    }
  }

</script>

<style>
  body {
    font-family: tahoma;
    color: #282828;
    margin: 0px;
  }

  .nav-bar {
    background: linear-gradient(-90deg, #84CF6A, #16C0B0);
    height: 60px;
    margin-bottom: 15px;
  }

  .cart {
    margin-right: 25px;
    float: right;
    border: 1px solid #d8d8d8;
    padding: 5px 20px;
  }

</style>
