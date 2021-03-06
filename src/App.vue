<template>
  <Header 
    @interval-change="updateInterval" 
    :darkTheme="darkTheme"
    @theme-change="updateTheme"
  />
  <main>
    <template v-if="loading">
      <p>Loading...</p>
    </template>
    <template v-else>
      <Table :ratesData="data"/>
    </template>
  </main>
</template>

<script>
import Header from '@/components/Header.vue'
import Table from '@/components/Table.vue'
import '@/styles/theme.scss'

export default {
  name: 'App',
  components: {
    Header,
    Table
  },
  data() {
    return {
      loading: true,
      fetchUrl: 'https://liquality.io/swap/agent/api/swap/marketinfo',
      data: [],
      intervalDuration: 5000,
      interval: null,
      darkTheme: false
    }
  },
  methods: {
    fetchData() {
      fetch(this.fetchUrl)
      .then(response => response.json())
      .then(data => {
        const modifiedData = data.map(item => {
          return {
            'from': item.from,
            'to': item.to,
            'rate': item.rate
          }
        })

        this.data = modifiedData 
        this.loading = false
      })
    },
    initInterval(duration) {
      // duration passed in milliseconds
      this.interval = setInterval(() => {
        this.fetchData()
      }, duration)
    },
    updateInterval(seconds) {
      const milliseconds = seconds * 1000
      this.intervalDuration = milliseconds

      clearInterval(this.interval)
      this.initInterval(milliseconds)
    },
    updateTheme(isDarkTheme) {
      this.darkTheme = isDarkTheme
      this.darkTheme
      ? document.body.classList.add(`theme-dark`)
      : document.body.classList.remove('theme-dark')
    }
  },
  mounted() {
    this.fetchData()
    this.initInterval(this.intervalDuration)
  },
  updated() {
    console.log('interval duration:',this.intervalDuration)
  }
}
</script>

<style lang="scss">
  @import './styles/theme.scss';

  body {
    margin: 0; 
    background-color: $white;

    h1, p, span {
      color: $blue-gray;
    }

    &.theme-dark {
      background-color: $darker-blue-gray;

      h1, p, span {
        color: $white;
      }
    }
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: $blue-gray;
    max-width: 90%;
    margin: 40px auto;
    
    @media screen and (min-width: 1280px) {
      margin: 64px auto;
    }
  }

  main {
    margin-top: 16px;

    @media screen and (min-width: 1280px) {
      margin-top: 32px;
    }
  }
</style>
