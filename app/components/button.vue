<template>
  <button class='voteButton btn' v-on:click='vote(info.id)' v-bind:style='{ background: info.color, color: info.text }'>
    {{ info.name }}
  </button>
</template>

<script>
import config from '../config/';

export default {
  props: ['info', 'show', 'alertshow'],
  data() {
    return {}
  },
  methods: {
    vote(id) {
      const body = {
        email: this.$cookie.get('email'),
        language: id,
      };

      this.$http.post(`${config.baseUrl}poll`, body)
        .then((res) => {
          this.alertshow('success', 'учтено 🔥, жми еще 👌', 1000)
        })
        .catch((res) => {
          this.alertshow('error', 'что-то пошло не так 💩', 5000)
        });
    },
  }
}
</script>

<style lang='scss'>
  .voteButton {
    width: 100%;
    height: 10vh;
    font-size: 3vh;
    display: inline-block;
    position: relative;
    border: none;
  }
  .btn {
    outline: none;
    border-radius: 5px;
    padding: 15px 25px;
    text-decoration: none;
    color: #fff;
    position: relative;
    display: inline-block;
  }

  .btn:active {
    transform: translate(0px, 5px);
    -webkit-transform: translate(0px, 5px);
    box-shadow: 0px 4px 0px 0px #000;
  }

</style>
