<template>
  <div>
    <div class="nav-bar"></div>
    <div class="product">
      <div class="product-image">
        <img :src="image"/>
      </div>

      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inventory > 10">In stock</p>
        <p v-else-if="inventory <= 10">Almost out</p>
        <p v-else>Out of stock</p>
        <p v-if="onSale">On Sale!</p>
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        <div v-for="variant in variants"
             :key="variant.variantId"
             class="color-box"
             :style="{ backgroundColor: variant.variantColor }"
             @mouseover="updateProduct(variant.variantImage)">
        </div>
      </div>
      <select>
        <option v-for="size in sizes">{{ size }}</option>
      </select>
      <button @click="addToCart" :disabled="inventory<=0" :class="{disabledButton: inventory<=0}">Add to Cart</button>
      <button @click="removeFromCart" :disabled="cart<=0" :class="{disabledButton: cart<=0}">Remove from Cart</button>

      <div class="cart">
        <p>Cart({{ cart }})</p>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        product: 'Socks',
        image: './dist/vmSocks-green.jpg',
        inventory: 8,
        onSale: false,
        details: ['80% cotton', '20% polyester', 'Gender-neutral'],
        variants: [
          {
            variantId: 2234,
            variantColor: 'green',
            variantImage: 'dist/vmSocks-green.jpg'
          },
          {
            variantId: 2235,
            variantColor: 'blue',
            variantImage: 'dist/vmSocks-blue.jpg'
          },
        ],
        sizes: ['S', 'M', 'L'],
        cart: 0
      }
    },
    methods: {
      addToCart: function () {
        this.cart += 1;
        this.inventory -= 1;
      },
      removeFromCart: function () {
        this.cart -= 1;
        this.inventory += 1;
      },
      updateProduct: function (variantImage) {
        this.image = variantImage;
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

  .product {
    display: flex;
    flex-flow: wrap;
    padding: 1rem;
  }

  img {
    border: 1px solid #d8d8d8;
    width: 70%;
    margin: 40px;
    box-shadow: 0px .5px 1px #d8d8d8;
  }

  .product-image {
    width: 80%;
  }

  .product-image,
  .product-info {
    margin-top: 10px;
    width: 50%;
  }

  .color-box {
    width: 40px;
    height: 40px;
    margin-top: 5px;
  }

  .cart {
    margin-right: 25px;
    float: right;
    border: 1px solid #d8d8d8;
    padding: 5px 20px;
  }

  button {
    margin-top: 30px;
    border: none;
    background-color: #1E95EA;
    color: white;
    height: 40px;
    width: 100px;
    font-size: 14px;
  }

  .disabledButton {
    background-color: #d8d8d8;
  }

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

  .tab {
    margin-left: 20px;
    cursor: pointer;
  }

  .activeTab {
    color: #16C0B0;
    text-decoration: underline;
  }
</style>
