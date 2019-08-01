<template>
 <div class="period-switcher-wrapper">
   <div v-on:click="changeSubsPrice(true)"><span v-bind:class="{active: this.clickedMonth}">{{btnMonthlyTitle}}</span></div>
   <div v-on:click="changeSubsPrice(false)" ref="yearBtn"><span v-bind:class="{active: this.clickedYear}">{{btnYearlyTitle}}</span></div>
 </div>
</template>

<script>
import {SUBS_MONTHLY, SUBS_YEARLY} from '../common/consts'

export default {
 props: {
   subscription: {
    type: Array
   }
  },
  data () {
    return {
     btnMonthlyTitle: SUBS_MONTHLY,
     btnYearlyTitle: SUBS_YEARLY,
     clickedMonth: false,
     clickedYear: false,
    }
  },
  methods: {
   changeMonthlySubs: function() {
    this.subscription.map(item => { 
    item.priceMonth = item.initialPriceMonth
    })
   },
   changeYearlySubs: function() {
    this.subscription.map(item => {
    const numRound = (item.initialPriceYear / 12).toFixed(2)
    item.priceMonth = parseFloat(numRound)
    })
   },
    changeSubsPrice: function(period) {
      this.subscription.map(item => {
        if (period) {
          item.period = period
          item.priceMonth = item.initialPriceMonth
          item.checkoutPrice = item.priceMonth
          this.clickedMonth = period
          this.clickedYear = !period
        } else {
          item.period = period
          item.priceMonth = parseFloat((item.initialPriceYear / 12).toFixed(2))
          item.checkoutPrice = item.initialPriceYear
          this.clickedYear = !period
          this.clickedMonth = period
        }
      })
    }
  },
  mounted() {
   this.$refs.yearBtn.click()
  }
}
</script>

<style>
 .period-switcher-wrapper {
    height: 60px;
    display: -ms-flexbox;
    display: flex;
    -ms-flex-align: center;
    align-items: center;
    -ms-flex-pack: center;
    justify-content: center;
 }
 .period-switcher-wrapper div{
    border: 1px solid #1580dd;
    color: #1580dd;
 }
 .period-switcher-wrapper div:first-of-type {
   border-radius: 4px 0 0 4px;
 }
 .period-switcher-wrapper div:nth-child(2){
   border-radius: 0 4px 4px 0;
 }
 .period-switcher-wrapper div > span {
    width: 100px;
    padding: 6px 20px;
    display: inline-block;
    cursor: pointer;
    -webkit-transition: background .2s ease-out;
    transition: background .2s ease-out;
 }
 .period-switcher-wrapper div > span:hover {
   background: rgba(21,  128,221,.15);
 }
 .active {
    color: #fff;
    background: #1580dd;
    cursor: default !important;
 } 

 .active:hover {
   background: #1580dd !important;
 }
</style>

