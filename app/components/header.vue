<template>
    <header>
      <p>🙀🤖<span><b>That's all folks</b></span>👌🤖🤖👏👮‍🍕</p>
      <counter-component></counter-component>
      <!-- <top-component></top-component> -->
    </header>
</template>

<script>
import counterComponent from './counter.vue';
import topComponent from './top.vue';

export default {
  components: {
    counterComponent,
    topComponent,
  },
};

</script>

<style lang='scss'>
  header {
    min-height: 10vh;
    display: block;
    vertical-align: middle;
    position: relative;
    text-align: left;
    padding: 0 0 25px;
    overflow: hidden;
    p {
      font-size: 4.5vh;
      display: inline-block;
      width: 65vw;
      text-align: left;
      color: #FFFFFF;
      font-weight: bold;
      vertical-align: middle;
      text-decoration: none;
      position: absolute;
      left: 0;
      top: 0;
    }
    a {
      color: #44c0ff;
      span {
        border-bottom: 1vh solid #44c0ff;
      }

    }
    .counter {
      text-align: right;
      width: 35vw;
      position: absolute;
      right: 0;
      top: 0;
      display: inline-block;
    }
  }


</style>