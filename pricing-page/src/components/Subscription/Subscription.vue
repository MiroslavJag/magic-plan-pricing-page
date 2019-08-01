<template>
 <div class="subscriptions">
   <h3>{{this.subsTitle}}</h3>
   <p>{{this.subsSubTitle}}</p>
   <subs-period-switcher v-bind:subscription="this.subscriptions"/>
   <div class="subs-wrapper">
     <li v-for="(item, index) in subscriptions" v-bind:key="index">
     <h3>{{item.name}}</h3>
     <h1>{{getCurrency(item.currency)}}{{item.priceMonth}}</h1>
     <p>{{item.plan}}</p>
     <button v-on:click="item.showCheckout = !item.showCheckout" class="subscribe-btn">{{subsBtnTitle}}</button>
     <div class="divider"/>
     <subs-checkout-price 
      v-show="item.showCheckout" 
      v-bind:data="{
        period: item.period,
        initialPriceMonth: item.initialPriceMonth,
        initialPriceYear: item.initialPriceYear,
        subName: item.name,
        priceMonth: item.priceMonth,
        checkoutPrice: item.checkoutPrice,
        currency: item.currency }"/>
     <div class="services-wrapper">   
      <p v-for="(service, index) in item.services" v-bind:key="index" class="services">{{service}}</p>
     </div>
   </li>
   </div>
 </div>
</template>

<script>
import PeriodSwitcher from '../Subscription/PeriodSwitcher'
import CheckoutPrice from '../Subscription/CheckoutPrice'
import {getCurrencyFromat} from '../common/helpers'
import {SUBS_TITLE, SUB_TITLE, SUBS_BUTTON} from '../common/consts'

export default {
  props: {
   subscriptions: {
    type: Array
   }
  },
  components: {
    'subs-period-switcher' : PeriodSwitcher,
    'subs-checkout-price' : CheckoutPrice
  },
  data () {
    return {
     subsTitle: SUBS_TITLE,
     subsSubTitle: SUB_TITLE,
     subsBtnTitle: SUBS_BUTTON,
     currency: null
    }
  },
  methods: {
    getCurrency: function(currency) {
      return getCurrencyFromat(currency)
    }
  }
}
</script>
<style>
 .subscriptions {
  display: flex;
  flex-direction: column;
  max-width: 700px;
  margin: 0 auto;
  text-align: center;
  background: white;
  padding: 22px 0;
  box-shadow: 0 0 30px 0 rgba(40,40,37,.15);
  border-radius: 4px;
  margin-bottom: 50px;
 }
 .subs-wrapper {
   display: flex;
   max-width: 700px;
   list-style-type: none;
   flex-direction: column;
 }
 .subscriptions h3:first-of-type  {
   font-size: 20px;
   font-weight: 700;
   color: #333;
 }
 .subscriptions p:first-of-type {
   padding: 18px 10px;
   color: #4a4a4a;
   font-size: 14px;
 }
 .subs-wrapper h3 {
    padding: 14px 0;
    background: #62b2eb;
    color: #fff !important;
    position: relative;
    line-height: 1.43;
 }
 .subs-wrapper li:nth-child(2) h3 {
    border-left: 1px solid rgba(240, 240, 240, 0.8);
 }
 .subs-wrapper li:nth-child(2) {
    border-left: 1px solid rgba(151, 151, 151, 0.3);
    margin-top: 80px;
 }
 .subs-wrapper h1 {
    padding-top: 14px;
    font-size: 36px;
    line-height: 1.43;
    font-weight: 400;
 }
 .subs-wrapper p {
    font-size: 14px;
 }
 .subs-wrapper .subscribe-btn{
    width: 160px;
    transition: background .2s ease-out;
    background-color: #1580dd;
    border-color: #1580dd;
    border-radius: 4px;
    padding: 8px 12px;
    font-size: 14px;
    line-height: 1.42857143;
    cursor: pointer;
    color: white;
    font-weight: 400;
    text-align: center;
    margin-bottom: 28px;
 }
 .subs-wrapper .subscribe-btn:hover {
   background-color: #1165ae;
   border-color: #1165ae;
 }
 
 .subs-wrapper .divider {
   margin: 0 10px;
   border-bottom: 1px solid #979797;
   opacity: .3;
 }
 .subs-wrapper .services {
   padding: 5px 0;
   line-height: 1.4;
 }

 .subs-wrapper .services-wrapper {
   padding-top: 28px;
 }
 .subs-wrapper .services-wrapper p {
    padding: 8px 5px;
 }

 @media  screen and (min-width: 768px) {
    .subs-wrapper {
      flex-direction: row;
    }
    .subs-wrapper li:nth-child(2) {
      margin-top: 0;
    }
  }
</style>
