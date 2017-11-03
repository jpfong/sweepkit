<template>
  <div class="hello">
   <div>{{ sweepstakes }} ({{ displaySweepstakesCount }})</div>
      <form v-on:submit="submitSweepstake()">
          <input type="text" v-model="name">
          <input type="submit" value="Submit">
      </form>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      sweepstakes: [],
      name: null
    }
  },
  mounted () {
    this.axios.get('/sweepstakes').then((response) => {
      this.sweepstakes = response.data.sweepstakes
    })
  },
  methods: {
    submitSweepstake () {
      this.axios.post('/sweepstakes', { name: this.name }).then((response) => {
        this.sweepstakes.push(response.data.sweepstake)
        this.name = null
      })
    }
  },
  computed: {
    displaySweepstakesCount () {
      return this.sweepstakes.length
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
