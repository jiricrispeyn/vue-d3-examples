<template>
  <div id="app">
    <simple-bar-graph :data="data" v-if="data" />
  </div>
</template>

<script>
import { csv } from 'd3-request'
import SimpleBarGraph from './components/SimpleBarGraph';

export default {
  name: 'app',
  components: {
    SimpleBarGraph
  },
  data() {
    return {
      data: null
    }
  },
  created() {
    csv('/src/assets/sales.csv', (error, data) => {
      if (error) {
        throw error;
      }

      data = data.map(d => Object.assign({}, d, { sales: +d.sales }));

      this.data = data;
    });
  }
}
</script>

<style lang="scss" scoped>
  .simple-bar-graph {
    width: 960px;
    height: 500px;
  }
</style>
