<template>
  <div>
    <div class="nav-bar"></div>
    <div class="cart">
      <p>Cart({{ cart }})</p>
    </div>
    <product @add-to-cart="addToCart"
             @remove-from-cart="removeFromCart"
             :is-cart="cart.length>0"/>
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
        cart: [],
        isCart: false
      }
    },
    methods: {
      addToCart: function (id) {
        //this.cart += 1;
        this.cart.push(id)
      },
      removeFromCart: function (id) {
        //this.cart -= 1;
        if(this.cart.includes(id)) {
          this.cart.splice(this.cart.indexOf(id), 1);
        }
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
