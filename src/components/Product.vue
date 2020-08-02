<template>
  <div class="product">
    <div class="product-image">
      <img :src="image"/>
    </div>

    <div class="product-info">
      <h1>{{ title }}</h1>
      <p v-if="inStock">In stock</p>
      <p v-else :class="{'out-of-stock': !inStock}">Out of stock</p>
      <p v-if="onSale">{{ isSale }}</p>
      <ul>
        <li v-for="detail in details">{{ detail }}</li>
      </ul>
      <div v-for="(variant, index) in variants"
           :key="variant.variantId"
           class="color-box"
           :style="{ backgroundColor: variant.variantColor }"
           @mouseover="updateProduct(index)">
      </div>
    </div>
    <select>
      <option v-for="size in sizes">{{ size }}</option>
    </select>
    <button @click="addToCart" :disabled="!inStock" :class="{disabledButton: !inStock}">Add to Cart</button>
    <button @click="removeFromCart" :disabled="cart<=0" :class="{disabledButton: cart<=0}">Remove from Cart</button>
  </div>
</template>

<script>
  export default {
    props: {
      cart: {
        type: Number
      }
    },
    data() {
      return {
        product: 'Socks',
        brand: 'Vue Mastery',
        selectedVariant: 0,
        onSale: false,
        details: ['80% cotton', '20% polyester', 'Gender-neutral'],
        variants: [
          {
            variantId: 2234,
            variantColor: 'green',
            variantImage: 'dist/vmSocks-green.jpg',
            variantQuantity: 10
          },
          {
            variantId: 2235,
            variantColor: 'blue',
            variantImage: 'dist/vmSocks-blue.jpg',
            variantQuantity: 0
          },
        ],
        sizes: ['S', 'M', 'L']
      }
    },
    methods: {
      addToCart: function () {
        this.$emit('add-to-cart');
      },
      removeFromCart: function () {
        this.$emit('remove-from-cart');
      },
      updateProduct: function (index) {
        this.selectedVariant = index;
      }
    },
    computed: {
      title() {
        return this.brand + ' ' + this.product;
      },
      image() {
        return this.variants[this.selectedVariant].variantImage;
      },
      inStock() {
        return this.variants[this.selectedVariant].variantQuantity;
      },
      isSale() {
        if (this.onSale) {
          return this.brand + ' ' + this.product + ' are on sale';
        }
      }
    }
  }
</script>

<style scoped>
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

  button {
    margin-top: 30px;
    border: none;
    background-color: #1E95EA;
    color: white;
    height: 40px;
    width: 100px;
    font-size: 14px;
  }

  .out-of-stock {
    text-decoration: line-through;
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
