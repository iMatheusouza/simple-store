<template>
  <Product
    :premium="premium"
    @addToCart="updateCart"
    @removeFromCart="removeFromCart"
    :cartIsEmpty="cartIsEmpty"
  />
  <div class="cart-counter">
    <span>Cart({{ cart.length }})</span>
  </div>
</template>

<script>
import Product from "./components/Product.vue";

export default {
  name: "App",
  components: {
    Product
  },
  data() {
    return {
      cart: [],
      premium: true
    };
  },
  methods: {
    updateCart(id) {
      this.cart.push(id);
    },
    removeFromCart(id) {
      if (this.cart.length > 0) {
        const deletedIndex = this.cart.findIndex(item => item === id);
        this.cart = this.cart.filter(
          (product, index) => index !== deletedIndex
        );
      }
    }
  },
  computed: {
    cartIsEmpty() {
      return this.cart.length === 0 ? true : false;
    }
  }
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  height: 100%;
  background-color: #f1f5f8;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  padding: 0 1rem;
  display: grid;
  grid-template-columns: 1fr auto;
}

div.cart-counter {
  span {
    background-color: white;
    padding: 0.5rem 1rem;
    display: block;
    width: fit-content;
    box-shadow: 0px 0px 1px 1px rgba(0, 0, 0, 0.2);
    margin-bottom: 0.5rem;
  }
}
</style>
