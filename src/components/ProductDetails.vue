<template>
  <div>
    <ul>
      <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'productDetails',
  props: {
    details: {
      type: Array,
      required: true
    }
  }
}
</script>
<style lang="css"></style>
