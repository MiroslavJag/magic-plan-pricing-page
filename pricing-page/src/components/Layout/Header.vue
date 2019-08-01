<template>
  <header>
    <h3>{{title}}</h3>
  </header>
</template>

<script>
import {PAGE_TITLE} from '../common/consts'

export default {
  data () {
    return {
      title: PAGE_TITLE 
    }
  }
}
</script>

<style>
  header {
    display: none;
  }
  header h3 {
    padding: 45px 20px;
    font-size: 31px;
    text-align: center;
    color: #1580dd;
    font-weight: 100;
  }
  @media  screen and (min-width: 768px) { 
    header {
      display: block;
    }
  }
</style>
