<template>
  <div 
    class="row" 
    :data-from="content.from" 
    :data-to="content.to"
  >
    <p class="type"> 
      <b>{{ content.from }}</b> to <b>{{ content.to }}</b>
    </p>
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
  @import '../styles/theme.scss';

  body {
    &.theme-dark {
      .row {
        background-color: $light-blue-gray;
      }
    }
  }

  .row {
    display: flex;
    align-items: center;
    text-align: left;
    gap: 16px;
    padding: 16px;
    border-radius: 5px;
    background-color: $light-gray;
  }

  .type {
    flex: 1.3;
    margin: 0;
  }

  .rate {
    flex: 1;
    justify-self: right;
    text-align: right;
  }
</style>