<template>
  <div>
    <input v-model="startDate" type="text"/>
    <input v-model="endDate" type="text"/>
    <button v-on:click="display()">Show me</button>
    <div>
      <div v-if="loading">
        Loading... Plase wait
      </div>
      <div v-else-if="error">
        Error
      </div>
      <div v-else>
        <asteroid-item v-bind:key="asteroid.name" v-for="asteroid in asteroids" :asteroid="asteroid"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import asteroidItem from '@/components/AsteroidItem'

export default {
  name: 'Asteroids',
  components: {
    'asteroid-item': asteroidItem
  },
  data () {
    return {
      startDate: '2015-09-07',
      endDate: '2015-09-09',
      key: 'bTGOPW97fJjxzaKqMZnFa9I0ouryxeO5JJnemhUg',
      asteroids: [],
      loading: false,
      error: false
    }
  },
  methods: {
    display () {
      this.loading = true
      axios.get(`https://api.nasa.gov/neo/rest/v1/feed
    ?start_date=${this.startDate}&end_date=${this.endDate}&api_key=${this.key}`)
        .then(response => response.data)
        .then(json => {
          let retrieved = []
          Object.keys(json.near_earth_objects).forEach(key => {
            let item = json.near_earth_objects[key]
            retrieved = retrieved.concat(item)
          })
          console.log(retrieved)
          this.asteroids = retrieved
          this.loading = false
          this.error = false
        })
        .catch(reason => {
          console.log(reason)
          this.error = true
          this.loading = false
        })
    }
  }
}
</script>

<style scoped>

</style>
