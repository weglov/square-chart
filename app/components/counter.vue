<template>
  <div class="counter">
    <div class='number'>
      <i-count-up
        v-if='poll'
        v-bind:start='poll'
        v-bind:end='end'
        :decimals='0'
        v-bind:decimals='decimals'
        v-bind:duration='duration'
        v-bind:options='options'
        :callback='callback'
      ></i-count-up>
    </div>
    <div class='totalrps' v-bind:style='{ height: height }'>
      <div class="innerwraprps">
        <h3>RPS 🙈</h3>
        <div class='totalrpsvolue'>
        <i-count-up
          v-bind:start='oldtotal'
          v-bind:end='total'
          :duration='120'
          v-bind:options='optionstotal'
        ></i-count-up>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import config from '../config/';
import _ from 'lodash';
import ICountUp from 'vue-countup-v2';

export default {
  components: {
    ICountUp
  },
  data() {
    return {
      poll: 6713852930,
      end: 6713852930,
      total: 0,
      oldtotal: 0,
      height: '30vh',
      duration: config.timer,
      decimals: 0,
      options: {
        useEasing: true,
        useGrouping: true,
        separator: ',',
        decimal: '.',
        prefix: '',
        suffix: ''
      },
      optionstotal: {
        useEasing: true,
        useGrouping: true,
        separator: ',',
        decimal: '.',
        prefix: '',
        suffix: ''
      }
    }
  },
  created () {
    // this.startPolling()
  },
  methods: {
    callback(ins) {
      // this.poll = ins.endVal;
    },
    fetchData(first) {
      this.$http({ url: `${config.baseUrl}poll`, method: 'GET', emulateJSON: true })
        .then((response) => {
          let count = _.toNumber(response.body.totalPollHits);
          // if (count > 10000 && count < 1000000) {
          //   count = count / 1000;
          //   this.options.suffix = 'к';
          // } else if (count > 1000000) {
          //   count = count / 1000000;
          //   this.options.suffix = 'м';
          //   this.decimals = 1;
          // } else {
          //   this.decimals = 0;
          //   this.options.suffix = '';
          // }

          if (first) {
            this.poll = count - count / 10;
            this.end = count;
            this.total = 240;
          }

          if (this.end !== count && this.end < count) {
            const ctx = _.floor((count - this.end) / 120);
            this.total = _.floor(ctx / 1000);
          }

          if (this.total > 200) {
            this.height = '40vh';
          } else if (this.total > 300) {
            this.height = '50vh';
          } else if (this.total > 400) {
            this.height = '60vh';
          }

          this.end = count;
        })
    },
    startPolling() {
      this.fetchData(true);
      setInterval(() => this.fetchData(), config.timerMS); 
    }
  }
}
</script>

<style lang='scss'>
  .counter {
    width: 30vw;
    overflow: hidden;
    .polls {
      font-weight: bold;
      display: inline-block;
      vertical-align: bottom;
      color: #e3e3e3;
      margin: 0;
      line-height: 1;
      background: url('../assets/giphy.gif') no-repeat;
      background-size: contain;
      height: 6vh;
      width: 5vw;
      margin-bottom: 2vh;
    }
    .number {
      line-height: 1;
      font-family: 'Avenir', Helvetica, Arial, sans-serif;
      display: inline-block;
      font-weight: bold; 
      font-style: normal; 
      font-size: 3.5rem;
      color: #fff;
      text-align: center;
    }
  }
  
  .totalrps {
    position: fixed;
    bottom: 0;
    right: 0;
    font-size: 4vh;
    width: 24vw;
    height: 25vh;
    text-align: center;
    background: #000;
    background: url('../assets/giphy2.gif') no-repeat top center;
    padding: 2vh 2vw 0;
    background-size: cover;
    h3 {
      text-shadow: 0px 4px 10px #000;
    }
  }
  .innerwraprps {
    position: absolute;
    bottom: 0;
    width: 24vw;
    padding: 2vh 2vw 0;
  }

  .totalrpsvolue {
    font-size: 10vh;
    color: red;
    padding: 1vh;
    font-weight: bold;
    text-shadow: 0px 4px 10px #000;
  }

  @media all and (max-width: 680px) {
    #sidebar {
      display: none;
    }
    header {
      position: relative;
      min-height: 10vh;
      .top {
        li:first-child {
          display: none;
        }
        li {
          display: block;
        }
        top: 0;
      }
      p, .top {
        display: block;
        width: 100%;
        position: relative;
        text-align: center;
      }
      .counter {
        width: 100%; 
        display: block;
        position: relative;
        text-align: center;
        .polls {
          height: 6vh;
          width: 15vw;
        }
      }
    }
  }
</style>
