<template>
  <div class="left-align">
    <hr />
    <hr />
    <div v-for="review in reviews" :key="review">
      <div>
        <label for="name"><strong> Name:-</strong></label>
        &nbsp;
        {{ review.name }}
      </div>
      <div>
        <label for="review"><b>Review:-</b></label>
        &nbsp;
        {{ review.review }}
      </div>
      <div>
        <label for="rating"><strong>Rating:-</strong></label>
        &nbsp;
        {{ review.rating }}
      </div>
      <hr />
    </div>
    <hr />
  </div>
</template>

<script>
export default {
  props: {
    reviews: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {};
  },
};
</script>

<style>
.left-align {
  text-align: left;
}
</style>
