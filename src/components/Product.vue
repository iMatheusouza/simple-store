<template>
  <main>
    <section>
      <figure>
        <img :src="image" alt="" />
      </figure>

      <ul v-if="reviews.length" class="user-review-container">
        <h3>Users Review</h3>
        <li :key="index" v-for="(review, index) in reviews">
          <p>
            <strong>{{ review.name }}</strong> Gave {{ review.rating }} stars
            for this product
          </p>
          <p>"{{ review.review }}"</p>
          <em
            >{{ review.name }}
            {{
              review.recommend
                ? "recommend this product"
                : "don't recommend this product"
            }}</em
          >
        </li>
      </ul>

      <FormReview @emitFormSubmit="submitForm" />
    </section>

    <section>
      <article>
        <h1>{{ title }}</h1>

        <h2 v-if="inStock">In stock</h2>
        <h2 v-else>Out of stock</h2>

        <h3>Shipping {{ shipping }}</h3>

        <ProductDetails :details="productDetails" />

        <ul class="product-variant">
          <li :key="format.id" v-for="(format, index) in productFormat">
            <img :src="format.variantImage" @mouseover="changeProduct(index)" />
          </li>
        </ul>

        <div class="buttons-container">
          <button
            @click="handleAddToCart()"
            :class="{ 'button-disabled': !inStock }"
          >
            Add to cart
          </button>

          <button
            @click="handleRemoveFromCart()"
            :class="{ 'button-disabled': cartIsEmpty }"
          >
            Remove from cart
          </button>
        </div>
      </article>
    </section>
  </main>
</template>

<script>
import ProductDetails from "./ProductDetails.vue";
import FormReview from "./FormReview.vue";

export default {
  name: "CharacterInfo",
  components: {
    ProductDetails,
    FormReview
  },
  props: {
    premium: {
      type: Boolean,
      required: true
    },
    cartIsEmpty: Boolean
  },
  data() {
    return {
      product: "Socks",
      brand: "Nike",
      onSale: true,
      productDetails: ["50% cotton", "30% wool", "20% polyester"],
      selectedVariant: 0,
      productFormat: [
        { id: 21983, variantImage: "./assets/meia-bolinha.webp", quantity: 10 },
        {
          id: 2983,
          variantImage: "./assets/meia-quadriculada.webp",
          quantity: 9
        }
      ],
      reviews: []
    };
  },
  methods: {
    handleAddToCart() {
      if (this.inStock) {
        this.$emit("addToCart", this.productFormat[this.selectedVariant].id);
      }
    },
    changeProduct(index) {
      this.selectedVariant = index;
    },
    handleRemoveFromCart() {
      this.$emit("removeFromCart", this.productFormat[this.selectedVariant].id);
    },
    submitForm(review) {
      // console.log(review);
      this.reviews.push(review);
      // console.log(this.reviews);
    }
  },
  computed: {
    title() {
      const titleConstructor = `${this.brand} ${this.product}`;
      return this.onSale ? `${titleConstructor} on Sale!` : titleConstructor;
    },
    image() {
      return this.productFormat[this.selectedVariant].variantImage;
    },
    inStock() {
      return this.productFormat[this.selectedVariant].quantity;
    },
    shipping() {
      return this.premium ? "free" : "$2.99";
    }
  }
};
</script>

<style lang="scss" scoped>
main {
  text-align: left;
  padding-left: 2rem;
  display: grid;
  grid-template-columns: auto 1fr;
  column-gap: 2rem;

  figure {
    box-shadow: 0px 0px 1px 1px rgba(0, 0, 0, 0.2);
    padding: 1rem;
    height: 463px;
    width: 347px;
    box-sizing: content-box;
  }

  h1 {
    font-size: 3rem;
    margin-bottom: 1rem;
  }

  h2,
  h3 {
    font-weight: normal;
    margin-bottom: 0.5rem;
  }

  li {
    text-decoration: none;
    list-style: none;
  }

  ul.product-variant {
    display: flex;
    li {
      margin-right: 0.25rem;
      img {
        width: 32px;
        height: 42.7px;
      }
    }
  }

  ul.user-review-container {
    margin-top: 2rem;
    h3 {
      font-weight: 600;
    }
    li {
      box-shadow: 0px 0px 1px 1px rgba(0, 0, 0, 0.2);
      padding: 1rem 2rem;
      background-color: white;
      margin-bottom: 1.5rem;
    }
  }

  button {
    background-color: palevioletred;
    color: white;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    margin: 0 auto;
    cursor: pointer;
  }

  button.button-disabled {
    background-color: gainsboro;
    cursor: not-allowed;
  }
}
</style>
