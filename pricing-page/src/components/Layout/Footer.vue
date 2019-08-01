<template>
  <footer>
    <p>{{copyright}}</p>
  </footer>
</template>

<script>
import {COPYRIGHT_TEXT} from '../common/consts'

export default {
  data () {
    return {
      copyright: COPYRIGHT_TEXT
    }
  }
}
</script>

<style>
  footer {
    text-align: center;
    background-color: #1580dd;
    color: #fff;
    width: 100%;
    padding: 5px 0;
    border: none;
    z-index: 1002;
    position: absolute;
    bottom: 0;
  }

  footer p {
    font-size: 14px;
    line-height: 1.42857143;
    padding: 0 15px;
  }
</style>
