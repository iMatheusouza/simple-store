<template>
  <ul>
    <li :key="detail" v-for="detail in details">
      {{ detail }}
    </li>
  </ul>
</template>

<script>
export default {
  name: "ProductDetails",
  props: {
    details: {
      type: Array,
      required: true
    }
  }
};
</script>

<style scoped lang="scss">
ul {
  padding-left: 1rem;
  margin-bottom: 1rem;
  li {
    text-decoration: none;
    list-style: none;
  }
}
</style>
