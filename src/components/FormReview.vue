<template>
  <form @submit.prevent="handleFormSubmit">
    <h2>Form Review</h2>
    <label for="">Name:</label>
    <input v-model="name" type="text" name="" id="name" />

    <label for="">Review:</label>
    <textarea v-model="review" name="" id="review"></textarea>

    <label for="">Rating:</label>
    <select v-model.number="rating" name="" id="">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
      <option value="4">4</option>
      <option value="5">5</option>
    </select>

    <fieldset>
      <legend>Would recommend this product?</legend>
      <label for="recommendTrue"
        >Sim

        <input
          v-model="recommend"
          :value="true"
          type="radio"
          name="recommend"
          id="recommendTrue"
        />
      </label>

      <label for="recommendFalse"
        >Não
        <input
          v-model="recommend"
          :value="false"
          type="radio"
          name="recommend"
          id="recommendFalse"
        />
      </label>
    </fieldset>

    <button type="submit">Send Review</button>
  </form>
</template>

<script>
export default {
  name: "FormReview",
  data() {
    return {
      name: "",
      review: "",
      rating: null,
      recommend: false
    };
  },
  methods: {
    handleFormSubmit() {
      if (this.name && this.review && this.rating) {
        let formReview = {
          name: this.name,
          review: this.review,
          rating: this.rating,
          recommend: this.recommend
        };

        console.log(formReview);
        this.$emit("emitFormSubmit", formReview);

        this.name = "";
        this.review = "";
        this.rating = null;
        this.recommend = false;
      } else {
        alert("Please fill the remaining data");
        return;
      }
    }
  }
};
</script>

<style scoped lang="scss">
form {
  margin-top: 5rem;
  background-color: white;
  box-shadow: 0px 0px 1px 1px rgba(0, 0, 0, 0.2);
  padding: 1rem 2rem;
  margin-bottom: 3rem;

  h2 {
    text-align: center;
    margin-bottom: 1.5rem;
  }

  textarea,
  input[type="text"],
  button,
  select,
  label {
    display: block;
    margin-bottom: 1rem;
  }

  fieldset {
    border: 0;
    legend {
      font-weight: 500;
      margin-bottom: 0.5rem;
    }

    input {
      margin-right: 0.5rem;
    }
  }
}
</style>
