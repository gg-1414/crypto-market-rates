<template>
  <div class="table">
    <Row 
      v-for="item in ratesData" 
      :key="`${item.from}-${item.to}`" 
      :content="item"
    />
  </div>
</template>

<script>
import Row from './Row.vue'

export default {
  name: 'Table',
  components: {
    Row
  },
  props: {
    ratesData: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style lang="scss" scoped>
  .table {
    display: grid;
    grid-template-columns: 1fr;
    gap: 16px;

    @media screen and (min-width: 768px) {
      grid-template-columns: repeat(2, 1fr);
    }

    @media screen and (min-width: 1280px) {
      grid-template-columns: repeat(4, 1fr);
    }
  }
</style>