<template>
  <div id="app">
    <simple-bar-graph />
  </div>
</template>

<script>
import SimpleBarGraph from './components/SimpleBarGraph';

export default {
  name: 'app',
  components: {
    SimpleBarGraph
  },
  data() {
    return {
      
    }
  }
}
</script>

<style lang="scss" scoped>
  .simple-bar-graph {
    width: 960px;
    height: 500px;
  }
</style>
