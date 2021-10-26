<template>
  <div id="app">
    <div>
      <label v-for="item in 5" v-bind:key="item">
        <input
            type="radio"
            v-bind:id="item"
            v-bind:value="item"
            v-model="picked"
        />
        {{ item }}
      </label>
      <hr/>
      <h3>{{ currentMeetup }}</h3>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      API_URL: "https://course-vue.javascript.ru/api",
      meetup: null,
      picked: null,
      events: [],
    }
  },
  beforeMount() {
    this.fetchMeetup()
  },
  computed: {
    currentMeetup() {
      return this.meetup ? this.meetup.title : ""
    }
  },
  watch: {
    picked(value) {
      this.meetup = this.events[value]
    }
  },
  methods: {
    fetchMeetup() {
      fetch(`${this.API_URL}/meetups`)
          .then((response) => response.json())
          .then((response) => {
            this.events = response
          })
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
