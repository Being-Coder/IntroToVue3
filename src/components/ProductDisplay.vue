<template>
  <div class="col-md-4 ImageBox">
    <div>
      <img :src="image" class="Img" />
    </div>
    <h2>{{ price }} /- only</h2>
  </div>
  <div class="col-md-4 InfoBox">
    <div class="anchor">
      <a :href="url" target="_blank"><b>Google.co.in</b></a>
    </div>
    <hr />
    <h2 style="color: black; font-family: fantasy">
      {{ productBrand }}
    </h2>
    <h4>{{ sale }}</h4>
    <h6>Shipping : {{ shipping }}</h6>
    <hr />
    <h3 v-if="quantity > 10">In stock</h3>
    <h3 v-else-if="quantity < 10 && quantity > 0">Almost sold out</h3>
    <h3 v-else>Out of stock</h3>
    <hr />
    <ul v-for="detail in details" :key="detail">
      <li>{{ detail }}</li>
    </ul>
    <hr />
    <div
      id="dressColorCircle"
      v-for="(varient, index) in varients"
      :key="varient.id"
      :style="{ backgroundColor: varient.color }"
      @mouseover="updateVarient(index)"
    ></div>
    <br />
    <button
      class="btn btn-primary btn-lg"
      :class="{ disabled: quantity == 0 }"
      @click="addToCart"
    >
      Add to cart</button
    >&nbsp;
    <button
      class="btn btn-warning btn-lg"
      :disabled="cartCount == 0 ? true : false"
      @click="this.$emit('removeFromCart', varients[selectedVarient].id)"
    >
      Remove from cart
    </button>
  </div>
  <div class="col-md-4 CommentBox">
    <product-review @ProductReview="ProductReview"></product-review>
    <all-reviews :reviews="reviews"></all-reviews>
  </div>
</template>

<script>
import ProductReview from "@/components/ProductReview.vue";
import AllReviews from "@/components/AllReviews.vue";
export default {
  components: {
    ProductReview,
    AllReviews,
  },
  props: {
    premium: {
      type: Boolean,
      required: true,
    },
    cart: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      count: 0,
      selectedVarient: 0,
      brand: "Vue Mastery",
      product: "Dress",
      url: "http://Google.co.in",
      details: ["50% cotton", "30% wool", "20% polyster"],
      varients: [
        {
          id: 2215,
          color: "blue",
          image: "/img/blue-dress.ad760567.jpg",
          quantity: 30,
          onSale: false,
          price: 1250,
        },
        {
          id: 2216,
          color: "red",
          image: "/img/red-dress.67dc220f.jpg",
          quantity: 10,
          onSale: true,
          price: 750,
        },
      ],
      reviews: [],
    };
  },
  methods: {
    ProductReview(review) {
      this.reviews.push(review);
      console.log(this.reviews);
    },
    addToCart() {
      this.$emit("addToCart", this.varients[this.selectedVarient].id);
    },
    updateVarient(index) {
      this.selectedVarient = index;
    },
  },
  computed: {
    cartCount() {
      return this.cart;
    },
    shipping() {
      if (this.premium) {
        return 0;
      }
      return 2.99;
    },
    productBrand() {
      return this.brand + " " + this.product;
    },
    image() {
      return this.varients[this.selectedVarient].image;
    },
    quantity() {
      return this.varients[this.selectedVarient].quantity;
    },
    sale() {
      if (this.varients[this.selectedVarient].onSale) {
        return this.productBrand + " is on sale.";
      }
      return this.productBrand + " sale will start soon.";
    },
    price() {
      return this.varients[this.selectedVarient].price;
    },
  },
};
</script>

<style>
li {
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  font-size: 20px;
}
#dressColorCircle {
  margin-left: 100px;
  text-align: left;
  background-color: burlywood;
  height: 70px;
  width: 70px;
  border-radius: 20px;
}
h3 {
  color: red;
  background-color: yellowgreen;
  margin-left: 150px;
  margin-right: 150px;
}
.SocksBox {
  padding: 15px;
}
.Img {
  width: 500px;
  height: 600px;
}
.ImageBox {
}
.InfoBox {
}
.CommentBox {
  width: 300px;
  margin-left: 75px;
}
.anchor {
  margin-left: 185px;
  margin-right: 185px;
  background-color: yellow;
  border: 1px solid black;
}
</style>
