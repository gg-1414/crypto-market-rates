<template>
  <div class="search-bar">
    <input type="text" placeholder="Search coin..." />
    <search-icon></search-icon>
  </div>
</template>

<script>
import SearchIcon from './icons/Search.vue'

export default {
  name: 'SearchBar',
  components: {
    SearchIcon
  }
}
</script>

<style lang="scss" scoped>
  @import '../styles/theme.scss';

  .search-bar {
    position: relative;
  }

  input {
    padding: 8px;
    font-size: 14px;
    outline: none;
    width: 100%;
    box-sizing: border-box;
    border: 1px solid $gray;
    border-radius: 3px;
  }

  svg {
    position: absolute;
    right: 12px;
    top: 50%;
    transform: translateY(-50%);
  }
</style>