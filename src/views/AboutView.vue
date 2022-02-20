<template>
  <div class="container-fluid SocksBox">
    <div class="row">
      <div style="text-align: right; padding-right: 80px">
        <strong>Cart : {{ cart.length }}</strong>
      </div>
      <ProductDisplay
        :cart="cart"
        :premium="premium"
        @addToCart="addToCart"
        @removeFromCart="removeFromCart"
      ></ProductDisplay>
    </div>
  </div>
</template>

<script>
import ProductDisplay from "../components/ProductDisplay.vue";
export default {
  components: {
    ProductDisplay,
  },
  data() {
    return {
      cart: [],
      premium: false,
    };
  },
  methods: {
    addToCart(id) {
      this.cart.push(id);
    },
    removeFromCart(id) {
      this.cart.pop(id);
    },
  },
};
</script>
<style scoped></style>
