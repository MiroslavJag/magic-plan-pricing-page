<template>
  <div class="content-wrapper">
    <app-header/>
    <app-content/>
    <app-footer/>
  </div>
</template>

<script>
import Header from './components/Layout/Header.vue'
import Content from './components/Layout/Content.vue'
import Footer from './components/Layout/Footer.vue'

export default {
  components: {
    'app-header' : Header,
    'app-content' : Content,
    'app-footer' : Footer
  },

  data () {
    return {
    }
  }
}
</script>

<style>

  * {
    margin: 0;
    padding: 0;
  }

  body {
    font-family: 'Noto Sans', sans-serif;
  }
  .content-wrapper {
    background-color: #f6f6f6;
    min-height: 100%;
    position: relative;
    overflow: hidden;
  }
</style>
