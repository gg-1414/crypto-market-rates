<template>
  <header>
    <img alt="Vue logo" src="https://liquality.io/images/LiqualityHorizontal.svg">
    <h1>Crypto Market Rates</h1>
    <div class="toggle-interval">
      <p>Refresh (seconds)</p>
      <button @click="handleIntervalClick" class="active">5</button>
      <button @click="handleIntervalClick">10</button>
      <button @click="handleIntervalClick">15</button>
    </div>
    <button class="toggle-theme" @click="handleToggleClick">
      <sun-icon v-if="!!darkTheme"/>
      <moon-icon v-else/>
    </button>
  </header>
</template>

<script>
import MoonIcon from './icons/Moon.vue'
import SunIcon from './icons/Sun.vue'

export default {
  name: 'Header',
  components: {
    MoonIcon,
    SunIcon,
  },
  props: {
    darkTheme: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    handleIntervalClick(event) {
      const activeButton = document.querySelector('.toggle-interval button.active')
      activeButton.classList.remove('active')
      event.target.classList.add('active')
      this.$emit('interval-change', event.target.innerText)
    },
    handleToggleClick() {
      this.$emit('theme-change', !this.darkTheme)
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '../styles/theme.scss';

  $toggle-theme-btn-width: 36px;

  body {
    &.theme-dark {
      .toggle-interval button {
        border: 2px solid $white;
      }
    }
  }

  button {
    cursor: pointer;
    -webkit-tap-highlight-color: transparent;
    &:focus { outline: none; }
  }

  header {
    display: grid;
    grid-template-columns: 1fr calc($toggle-theme-btn-width + 16px);
    grid-template-areas: 
      "logo themeToggle"
      "title title"
      "intervalToggle intervalToggle";

    h1 {
      font-size: 28px;
      grid-area: title;
      margin: 16px auto 12px;
    }

    img {
      justify-self: start;
      grid-area: logo;
    }

    .toggle-interval {
      grid-area: intervalToggle;
    }

    .toggle-theme {
      grid-area: themeToggle;
      justify-self: end;
    }

    @media screen and (min-width: 768px) {
      grid-template-columns: repeat(2, 1fr);

      img,
      h1 {
        justify-self: left;
      }

      h1 {
        grid-area: 2 / 1;
        margin-left: 0;
      }

      .toggle-interval {
        justify-self: right;
      }

      .toggle-interval {
        grid-area: 2 / 2;
      }
    }

    @media screen and (min-width: 1280px) {
      display: grid;
      grid-template-columns: auto auto auto calc(#{$toggle-theme-btn-width} + 24px);
      grid-template-rows: 1fr;
      align-items: center;
      
      h1 {
        font-size: 32px;
        grid-area: 1 / 2;
        justify-self: center;
      }

      .toggle-interval {
        grid-area: 1 / 3;
      }

      .toggle-theme {
        grid-area: 1 / 4;
      }
    }
  }

  .toggle-interval {
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
      color: $white;
      font-weight: bold;
      letter-spacing: 1px;
      background: $light-blue-gray;
      border: 2px solid $darkest-blue-gray;

      &:hover,
      &.active {
        background: linear-gradient(45deg, $teal, $magenta);
      }
    }

    @media screen and (min-width: 768px) {
      justify-content: right;
    }
  }

  .toggle-theme {
    border: none;
    height: 32px;
    width: $toggle-theme-btn-width;
    display: flex;
    align-items: center;
    border-radius: 5px;
    align-self: center;
    background-color: $light-gray;

    svg {
      width: 100%;
    }
  }
</style>