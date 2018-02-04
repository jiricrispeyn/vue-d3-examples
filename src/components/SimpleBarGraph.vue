<template>
  <div class="simple-bar-graph">
    <svg ref="svg" :width="width + margin.left + margin.right" :height="height + margin.top + margin.bottom">
      <g :style="{ 'transform': `translate(${margin.left}px, ${margin.top}px)` }">
        <rect class="bar" v-for="(item, index) in data" :key="index" :x="x(item.salesperson)" :width="x.bandwidth()" :y="y(item.sales)" :height="height - y(item.sales)" />
        <g ref="xAxis" :style="{ 'transform': `translate(0, ${height}px)` }" />
        <g ref="yAxis" />
      </g>
    </svg>
  </div>
</template>

<script>
import { scaleBand, scaleLinear } from 'd3-scale';
import { axisBottom, axisLeft } from 'd3-axis';
import { select } from 'd3-selection';
import { max } from 'd3-array';

export default {
  name: 'simple-bar-graph',
  props: {
    data: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      width: 0,
      height: 0,
      margin: { top: 20, right: 20, bottom: 30, left: 40 },
      x: scaleBand(),
      y: scaleLinear(),
      xAxis: axisBottom(),
      yAxis: axisLeft()
    }
  },
  mounted() {
    this.width = this.$el.getBoundingClientRect().width - this.margin.left - this.margin.right;
    this.height = this.$el.getBoundingClientRect().height - this.margin.top - this.margin.bottom;

    this.x.range([0, this.width])
          .padding(.1);
    this.y.range([this.height, 0]);

    this.update(this.data);
  },
  methods: {
    update(data) {
      this.x.domain(data.map(d => d.salesperson));
      this.y.domain([0, max(data, d => d.sales)]);

      this.xAxis.scale(this.x);
      this.yAxis.scale(this.y);

      select(this.$refs.xAxis).call(this.xAxis);
      select(this.$refs.yAxis).call(this.yAxis);
    }
  }
}
</script>

<style lang="scss" scoped>
.bar {
  fill: steelblue;
}
</style>
