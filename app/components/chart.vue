<template>
  <div>
    <header-component></header-component>
    <div class='table-chart'>
    <div id='chart'></div>
      <div id='sidebar'>
        <toprps></toprps>
      </div>
    </div>
  </div>
</template>

<script>
import config from '../config/';
import sample_data from '../config/data.js';
import _ from 'lodash';
import headerComponent from './header.vue';
import toprps from './topRPS.vue';


export default {
  components: {
    headerComponent,
    toprps,
  },
  data() {
    return {
      sample: sample_data,
      chart: '',
    }
  },
  mounted() {
    this.startPolling()
  },
  methods: {
    renderChart() {
      this.chart =d3plus.viz()
        .container('#chart')
        .data(this.sample)
        .type('tree_map')
        .id('id')
        .color('color')
        .text('name')
        .size('value')
        .messages(false)
        .mouse({                
          'move': false,
          'click': false,
        })
        .font({ weight: 'bold', family: 'arial', 'text-transform': "uppercase" })
        .background('#323232')
        .class((d) => {
          const font = `font${_.floor(d.d3plus.width, -2)}`;
          if (d.d3plus.height > 200) {
            return font;
          }

          return null;
        })
        .labels({
          align: 'middle',
          valign: 'top',
        })
        .legend(false)
        .draw();
    },
    reRender() {
      this.chart
        .data(this.sample)
        .draw();
    },
    getResult(first) {
      this.$http({ url: `${config.baseUrl}poll?full=true`, method: 'GET', emulateJSON: true })
        .then((response) => {
          const votes = _.get(response, 'body.votes');
          this.sample = _.map(this.sample, (val, key) => {
            val.value = votes[val.id];
            return val;
          });

          if (first) return this.renderChart();

          return this.reRender();
        })
    },
    startPolling() {
      this.getResult(true);
      setInterval(() => this.getResult(), config.rerender); 
    }
  }
}
</script>

<style lang='scss'>
.table-chart {
  display: table;
}
  #chart {
    width: 75vw;
    height: 80vh;
    position: relative;
    display: table-cell;
    vertical-align: top;
    > div {
      margin: 0 auto;
    }
    text {
      text-transform: uppercase;
    }
  }
  #sidebar {
    width: 20vw;
    display: table-cell;
    vertical-align: top;
    position: relative;
  }
  .font700, .font600, .font800 {
    text.d3plus_label {
      font-size: 90px !important;
    }
  }
  .font900, .font1000 {
    text.d3plus_label {
      font-size: 140px !important;
    }
  }
  .font500, .font400 {
    text.d3plus_label {
      font-size: 70px !important;
    }
  }
</style>