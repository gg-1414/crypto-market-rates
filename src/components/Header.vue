<template>
  <header>
    <img alt="Vue logo" src="https://liquality.io/images/LiqualityHorizontal.svg">
    <h1>Crypto Market Rates</h1>
    <div class="interval-toggle">
      <p>Refresh (seconds)</p>
      <button @click="handleClick" class="active">5</button>
      <button @click="handleClick">10</button>
      <button @click="handleClick">15</button>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header',
  methods: {
    handleClick(event) {
      const activeButton = document.querySelector('.interval-toggle button.active')
      activeButton.classList.remove('active')
      event.target.classList.add('active')
      this.$emit('interval-change', event.target.innerText)
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '../styles/theme.scss';

  header {
    display: grid;

    h1 {
      font-size: 24px;
    }

    img {
      justify-self: center;
    }

    @media screen and (min-width: 768px) {
      grid-template-columns: repeat(2, 1fr);

      img,
      h1 {
        justify-self: left;
      }

      h1 {
        grid-area: 2 / 1;
      }

      .interval-toggle {
        justify-self: right;
      }

      .interval-toggle {
        grid-area: 2 / 2;
      }
    }

    @media screen and (min-width: 1280px) {
      display: flex;
      justify-content: space-between;
      
      h1 {
        font-size: 32px;
      }
    }
  }

  .interval-toggle {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 6px;

    p {
      margin-right: 4px;
    }

    button {
      border-radius: 50%;
      height: 32px;
      width: 32px;
      color: white;
      font-weight: bold;
      letter-spacing: 1px;
      background: #4d6074;
      border: 2px solid black;
      cursor: pointer;

      &:hover,
      &.active {
        background: linear-gradient(45deg, $teal, $magenta);
      }

      &:focus {
        outline: none;
      }
    }

    @media screen and (min-width: 768px) {
      justify-content: right;
    }
  }
</style>