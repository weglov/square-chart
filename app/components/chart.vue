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
      votes: { "0":705991644,"1":16930488,"2":3041851396,"3":670149141,"4":100201422,"5":109766605,"6":481494543,"7":314839313,"8":75696198,"9":1270656457 },
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
      const votes = this.votes;
        this.sample = _.map(this.sample, (val, key) => {
          val.value = votes[val.id];
          return val;
        });

      return this.renderChart();
    },
    startPolling() {
      this.getResult(true);
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