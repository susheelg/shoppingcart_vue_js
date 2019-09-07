<template>
  <div>
    <div class="product">
      <div class="product-image">
        <img :src="image" />
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <p>Shipping: {{ shipping }}</p>

        <productDetails :details="details"></productDetails>

        <div
          class="color-box"
          v-for="(variant, index) in variants"
          :key="variant.variantId"
          :style="{ backgroundColor: variant.variantColor }"
          @mouseover="updateProduct(index)"
        ></div>

        <button
          v-on:click="addToCart"
          :disabled="!inStock"
          :class="{ disabledButton: !inStock }"
        >Add to cart</button>

        <button
          v-on:click="removeFromCart"
          :disabled="!inStock"
          :class="{ disabledButton: !inStock }"
        >Remove</button>
      </div>

      <producttabs :reviews="reviews"></producttabs>
    </div>
  </div>
</template>

<script>
import productDetails from './ProductDetails.vue'
import producttabs from './ProductTabs.vue'
export default {
  name: 'product',
  components: {
    productDetails,
    producttabs
  },
  props: {
    premium: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      brand: 'Patanjali',
      product: 'Socks',
      details: ['80% cotton', '20% polyester', 'Gender-neutral'],
      variants: [
        {
          variantId: 2234,
          variantColor: 'green',
          variantImage: '/vmSocks-green-onWhite.jpg',
          variantQuantity: 10
        },
        {
          variantId: 2235,
          variantColor: 'blue',
          variantImage: '/vmSocks-blue-onWhite.jpg',
          variantQuantity: 0
        }
      ],
      // cart: 0,
      selectedVariant: 0,
      reviews: []
    }
  },

  methods: {
    addToCart() {
      this.$emit('add-to-cart', this.variants[this.selectedVariant].variantId)
    },
    removeFromCart() {
      this.$emit(
        'remove-from-cart',
        this.variants[this.selectedVariant].variantId
      )
    },
    updateProduct(index) {
      this.selectedVariant = index
      console.log(index)
    }
  },
  computed: {
    title() {
      return this.brand + ' ' + this.product
    },
    image() {
      return this.variants[this.selectedVariant].variantImage
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity
    },
    shipping() {
      if (this.premium) {
        return 'Free'
      } else {
        return 100
      }
    }
  },
  mounted() {
    window.eventBus.$on('review-submitted', productReview => {
      this.reviews.push(productReview)
    })
  }
}
</script>
