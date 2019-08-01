<template>
 <div class="wrapper-checkout">
   <div class="checkout-section-wrapper">
     <div v-show="showCheckoutPrice()" class="checkout-section">
        <p v-show="this.data.subName !=='Standard' ? true : false">{{devicesTitle}}</p>
      <div v-show="this.data.subName !=='Standard' ? true : false">
        <div>
          <i v-on:click="decreaseCheckoutPrice()" v-bind:class="{disabled: this.disableButton}"  class="fas fa-minus-circle"></i>
          <p class="counter">{{counter}}</p>
          <i v-on:click="increaseCheckoutPrice()" class="fas fa-plus-circle"></i>
        </div>
      </div>
      <p class="checkout-sum" v-bind:class="{standard: this.data.subName === 'Standard'}">
        {{this.currency}}{{this.checkoutPriceSum}}
        <span v-show="this.data.subName ==='Standard' ? true : false"> / Year</span>
        </p>
     </div>
   </div>
   <div class="checkout-btns-wrapper"> 
     <button v-on:click="goToCheckout()" id="show-modal" @click="showModal = true" class="btn-paypal">
        <img src="../../assets/paypal-logo.png" />
      </button>
      <p>{{this.or}}</p>
      <button v-on:click="goToCheckout()" id="show-modal" @click="showModal = true" class="btn-credit-card">
        <i class="fas fa-credit-card"></i>{{checkoutCardText}}
      </button>
   </div>
   <modal v-if="showModal" @close="showModal = false" v-bind:paymentData="this.paymentData">
     <p slot="header">{{paymentText}}</p>
   </modal>
 </div>
</template>

<script>
import Modal from '../common/Modal'
import {getCurrencyFromat} from '../common/helpers'
import {DEVICES, CREDIT_CARD, CONFIRM_PAYMENT_TEXT, SUBS_MONTHLY, SUBS_YEARLY, OR} from '../common/consts'

export default {
components: {
  'modal' : Modal,
 },
 props: {
   data: {
    period: {type: Boolean},
    initialPriceMonth: {type: Number},
    initialPriceYear: {type: Number},
    priceMonth: {type: Number},
    subName: {type: String},
    checkoutPrice: {type: Number},
    currency: {type: String}
    }
  },
  data () {
    return {
     devicesTitle: DEVICES,
     counter: 1,
     disableButton: true,
     checkoutPriceSum: 0,
     checkoutCardText: CREDIT_CARD,
     showModal: false,
     paymentText: CONFIRM_PAYMENT_TEXT,
     monthly: SUBS_MONTHLY,
     yearly: SUBS_YEARLY,
     or: OR,
     paymentData: {},
     currency: null
    }
  },
  methods: {
   increaseCheckoutPrice: function() {
     this.disableButton = false
     this.counter += 1
     if (this.data.period) {
       this.checkoutPriceSum = parseFloat((this.checkoutPriceSum + this.data.priceMonth).toFixed(2))
     } else {
       this.checkoutPriceSum = parseFloat((this.checkoutPriceSum + this.data.initialPriceYear).toFixed(2))
     }
     console.log(this.counter)
   },
   decreaseCheckoutPrice: function() {
    if (this.counter == 1) {
     this.disableButton = true
    } else {
     this.counter -=1
     if (this.counter == 1) {
     this.disableButton = true
    }else if (this.period) {
       this.checkoutPriceSum = parseFloat((this.checkoutPriceSum - this.data.priceMonth).toFixed(2))
     } else {
       this.checkoutPriceSum = parseFloat((this.checkoutPriceSum - this.data.initialPriceYear).toFixed(2))
     }
    }
    console.log(this.counter)
   },
   showCheckoutPrice: function() {
    const priceYear = parseFloat((this.data.initialPriceYear / 12).toFixed(2))
    return this.data.subName === "Standard" && (this.data.priceMonth !== priceYear) ? false : true
   },
   goToCheckout: function() {
    this.paymentData["payment"] = {
      "subscription" : this.data.subName, 
      "period" : this.data.period ? this.monthly : this.yearly, 
      "price:" : this.checkoutPriceSum,
      "currency": this.data.currency
      }
   }
  },

  mounted () {
    if (this.data.period) {
      this.checkoutPriceSum = this.data.initialPriceYear
    } else {
      this.checkoutPriceSum = this.data.initialPriceMonth
    }
    this.currency = getCurrencyFromat(this.data.currency)
  },
  updated () {
    if (this.data.period) {
      this.checkoutPriceSum = parseFloat((this.data.priceMonth * this.counter).toFixed(2))
    } else {
      this.checkoutPriceSum = parseFloat((this.data.initialPriceYear * this.counter).toFixed(2))
    }
  },
}
</script>

<style>
  #show-modal {
    padding: 8px 14px;
    border-radius: 4px;
    width: 95%;
    border-color: #1580dd;
    transition: background .2s ease-out;
    background: #f6f6f6;
  }

  #show-modal:hover {
    background: rgba(21, 128,221,.15);
  }
  .btn-paypal img {
    height: 20px;
  }
  .btn-credit-card {
    font-size: 14px;
    line-height: 1.4;
    padding: 9.7px;
    color: #1580dd;
  }
  .btn-credit-card i {
    margin-right: 8px;
  }
  .checkout-btns-wrapper {
    background-color: #f6f6f6;
    padding: 18px 0px;
  }
  .wrapper-checkout div.checkout-btns-wrapper:nth-child(2) {
    border-left: 1px solid rgba(151, 151, 151, 0.3);
  }
  .checkout-btns-wrapper p {
    padding: 10px;
  }
  .checkout-section-wrapper{
    height: 53px;
  }
  .checkout-section {
    display: flex;
  }
  .checkout-section div:first-of-type {
    display: flex;
    flex: 2;
    justify-content: center;
  }
  .checkout-sum {
    padding: 18px 10px;
  }
  .checkout-section i {
    font-size: 16px;
    color: #6d6d6d;
    padding: 18px 10px;
  }
  .standard {
    flex: 1 !important;
  }
  .disabled {
    cursor: not-allowed;
    color: #ccc !important;
  }
  .counter {
    padding: 18px 5px !important;
  }
</style>
