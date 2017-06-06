<template>
<div style='text-align: right;'>
  <div class='toprps' v-if='users.length'>🔥 TOP 5:</div>
  <ul class='toprps-list' v-if='users.length'>
    <li v-for="(item, index) in users">
      <div class="item-number">{{ index + 1 }}.</div>
      <div class="item-email">{{ item.email }}</div>
      <div class="item-rps">~ {{ item.rps }} rps<br>{{ item.k }}</div>
    </li>
  </ul>
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
      users: [
      {"email":"ivan@...","count":2157022717},
      {"email":"burik666@...","count":1493273289},
      {"email":"256@...","count":702322627},
      {"email":"alarkin@...","count":534157110},
      {"email":"odn@...","count":484233343}],
      options: {
        useEasing: true,
        useGrouping: true,
        separator: ',',
        decimal: '.',
        prefix: '',
        suffix: 'rps'
      }
    }
  },
  created() {
    this.users = _.map(this.users, (v) => {
      const count = _.floor(v.count / 25200);
      const countk = _.floor(v.count / 1000000);
      return _.assign(v, { rps: count, k: `${countk} mln` })
    })
  },
  methods: {
  }
};
</script>

<style lang='scss'>
  .toprps {
    font-weight: bold;
    font-size: 5vh;
    margin-top: 3vh;
    text-align: center;
  }
  .toprps-list {
    display: block;
    padding: 2vh 0 2vh 2vw;
    li {
      display: table;
      border-bottom: 2px solid #515151;
      width: 100%;
      text-align: left;
      padding: 1vh 0;
      margin: 0;
      div {
        display: table-cell;
        text-align: left;
      }
      .item-number {
        font-weight: bold;
        color: yellow;
        width: 2vw;
      }
      .item-email {
        width: 7vw;
        overflow: hidden;
      }
      .item-rps {
        color: red;
        font-size: 2vh;
        font-weight: bold;
        text-align: right;
            width: 10vw;
      }
    }
  }
  @media all and (max-width: 680px) {
    .totalrps {
      width: 100%;
      padding: 2vh 2vw;
    }
  }
</style>