<template>
  <div class="simple-bar-graph">
    <svg ref="svg" :width="width + margin.left + margin.right" :height="height + margin.top + margin.bottom">
      <g :style="{ 'transform': `translate(${margin.left}px, ${margin.top}px)` }">
      </g>
    </svg>
  </div>
</template>

<script>
import { scaleBand, scaleLinear } from 'd3-scale';
import { select } from 'd3-selection';

export default {
  name: 'simple-bar-graph',
  data() {
    return {
      width: 0,
      height: 0,
      margin: { top: 20, right: 20, bottom: 30, left: 40 },
      x: scaleBand(),
      y: scaleLinear()
    }
  },
  mounted() {
    this.width = this.$el.getBoundingClientRect().width - this.margin.left - this.margin.right;
    this.height = this.$el.getBoundingClientRect().height - this.margin.top - this.margin.bottom;

    this.x.range([0, this.width]);
    this.y.range([this.height, 0]);
  }
}
</script>

<style>

</style>
