<template>
 <div class="content">
   <app-subscription v-bind:subscriptions="subscriptions"/>
 </div>
</template>

<script>
import Subscription from '../Subscription/Subscription'
import {SUBS_STANDARD, SUBS_BUSSINES, CURRENCY, PLAN_STANDARD, PLAN_BUSSINES, CHECKOUT_STANDARD, CHECKOUT_BUSSINES, SERVICES_STANDARD, SERVICES_BUSSINESS, PRICE_MONTH_STANDARD, PRICE_YEAR_STANDARD, PRICE_MONTH_BUSSINESS, PRICE_YEAR_BUSSINESS} from '../common/consts'

export default {
  components: {
    'app-subscription' : Subscription
  },
  data () {
    return {
     subscriptions: [
      {
        name: SUBS_STANDARD,
        initialPriceMonth: PRICE_MONTH_STANDARD,
        initialPriceYear: PRICE_YEAR_STANDARD,
        priceMonth: 0,
        priceYear: 0,
        checkoutPrice: 0,
        period: false,
        currency: CURRENCY,
        plan: PLAN_STANDARD,
        showCheckout: false,
        checkout: CHECKOUT_STANDARD,
        services: SERVICES_STANDARD
       },
      { name: SUBS_BUSSINES, 
        initialPriceMonth: PRICE_MONTH_BUSSINESS,
        initialPriceYear: PRICE_YEAR_BUSSINESS, 
        priceMonth: 0,
        priceYear: 0,
        checkoutPrice: 0,
        period: false,
        currency: CURRENCY,
        plan: PLAN_BUSSINES,
        showCheckout: false,
        checkout: CHECKOUT_BUSSINES,
        services: SERVICES_BUSSINESS
       }
     ]
    }
 }
}
</script>

<style>
  .content {
    text-align: center;
  }
</style>