<template>
  <div class="row">
    <div class="type"> 
      <b>{{ content.from }}</b> to <b>{{ content.to }}</b>
    </div>
    <span class="rate">{{ content.rate }}</span>
  </div>
</template>

<script>
export default {
  name: 'Row',
  props: {
    content: {
      type: Object,
      default: () => {}
    },
  }
}
</script>

<style lang="scss" scoped>
  .row {
    display: flex;
    align-items: center;
    text-align: left;
    gap: 16px;
    background-color: #eee;
    padding: 16px;
  }

  .type {
    flex: 1.3;
  }

  .rate {
    flex: 1;
    justify-self: right;
    text-align: right;
  }
</style>