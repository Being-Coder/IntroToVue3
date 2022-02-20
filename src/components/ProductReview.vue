<template>
  <hr />
  <div>
    <form @submit.prevent="submitReview">
      <div class="mb-3">
        <label for="name" class="form-label">Name : </label>
        <input type="name" class="form-control" id="name" v-model="name" />
      </div>
      <div class="mb-3">
        <label for="review" class="form-label">Review : </label>
        <textarea
          type="review"
          class="form-control"
          id="review"
          v-model="review"
        />
      </div>
      <div style="text-align: left">
        <label for="rating" class="form-label">Rating : </label>
        <select v-model="rating" class="form-control">
          <option value="1">*</option>
          <option value="2">* *</option>
          <option value="3">* * *</option>
        </select>
      </div>
      <hr />
      <hr />
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      review: "",
      rating: "",
    };
  },
  methods: {
    submitReview() {
      let productReview = {
        name: this.name,
        review: this.review,
        rating: this.rating,
      };
      this.$emit("ProductReview", productReview);
      (this.name = ""), (this.review = ""), (this.rating = "");
    },
  },
};
</script>

<style></style>
