<template>
  <div>

    <a href="#" class="toggle" v-on:click.prevent="toggle()">{{link}}</a>
    <div v-if="expanded">
      <ul>
        <li>
          {{name}}
        </li>
        <li>
          {{absolute}}
        </li>
      </ul>
    </div>
    <div v-else>
      {{asteroid.name}}
    </div>
  </div>
</template>

<script>
export default {
  name: 'AsteroidItem',
  props: ['asteroid'],
  computed: {
    link () {
      return this.expanded ? 'less' : 'more'
    },
    absolute () {
      return `Absolute ${this.asteroid.absolute_magnitude_h}`
    },
    name () {
      return `Name ${this.asteroid.name}`
    }
  },
  data () {
    return {
      expanded: false
    }
  },
  methods: {
    toggle () {
      this.expanded = !this.expanded
      console.log(this.expanded)
    }
  }
}
</script>

<style scoped>

</style>
