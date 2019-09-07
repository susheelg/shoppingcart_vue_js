<template>
  <div>
    <div>
      <span
        class="tabs"
        :class="{ activeTab: selectedTab === tab }"
        v-for="(tab, index) in tabs"
        :key="index"
        @click="selectedTab = tab"
        >{{ tab }}</span
      >

      <div v-show="selectedTab === 'Reviews'">
        <p v-if="!reviews.length">Their are no review yet</p>
        <ul>
          <li v-for="(review, index) in reviews" :key="index">
            <p>Name: {{ review.name }}</p>
            <p>Review: {{ review.review }}</p>
            <p>Rating: {{ review.rating }}</p>
          </li>
        </ul>
      </div>

      <div v-show="selectedTab === 'Make a review'">
        <productReviews></productReviews>
      </div>
    </div>
  </div>
</template>

<script>
import productReviews from '@/components/ProductReview.vue'
export default {
  name: 'producttabs',
  components: {
    productReviews
  },
  props: {
    reviews: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      tabs: ['Reviews', 'Make a review'],
      selectedTab: 'Reviews'
    }
  }
}
</script>

<style lang="scss" scoped></style>
