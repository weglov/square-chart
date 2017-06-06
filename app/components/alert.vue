<template>
    <div v-if='show' class='alert' v-bind:class='type'>{{ text }}</div>
</template>

<script>
import _ from 'lodash';


export default {
  props: ['show', 'text', 'type'],
}
</script>

<style lang='scss'>
  .alert {
    background-image: radial-gradient(ellipse farthest-side at 50% 100%,#b20000,rgba(178,0,0,0));
    height: 20vh;
    position: fixed;
    bottom: 0;
    font-size: 3vh;
    padding-top: 10vh;
    margin: 0;
    width: 100%;
    left: 0;
    right: 0;
    color: #fff;
    &.success {
      background-image: radial-gradient(ellipse farthest-side at 50% 100%,#13a230,rgba(178,0,0,0));
    }
  }
</style>
