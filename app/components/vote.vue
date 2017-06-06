<template>
  <div id='app_vote' class='fix-width'>
    <header-admin></header-admin>
    <div class='button_item' v-for='item in data'>
      <button-component v-bind:show='show' v-bind:alertshow='alertShow' v-bind:info='item'></button-component>  
    </div>
    <alert v-bind:show='show' v-bind:text='text' v-bind:type='type'></alert>
  </div>
</template>

<script>
import _ from 'lodash';
import sample_data from '../config/data.js';
import buttonComponent from './button.vue';
import alert from './alert.vue';
import headerAdmin from './headerAdmin.vue';


export default {
  components: {
    buttonComponent,
    headerAdmin,
    alert,
  },
  data() {
    return {
      data: sample_data,
      show: false,
      text: 'что-то пошло не так 💩',
      type: 'error',
    }
  },
  created() {
    return this.$router.push('/register');
  },
  methods: {
    alertShow(type, text, timer = 15000) {
      this.show = true;
      this.type = type;
      this.text = text;

      setTimeout(() => this.show = false, timer);
    },
  },
}
</script>

<style lang='scss'>
  .button_item {
    display: inline-block;
    width: 50%;
    padding: 2vh;
    margin: 0;
  }
  .logout {
    padding: 20px;
    display: block;
    text-decoration: underline;
  }
</style>
