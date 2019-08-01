<template id="modal-template">
  <transition name="modal">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">

          <div class="modal-header">
            <slot name="header">
              default header
            </slot>
          </div>

          <div class="modal-body">
            <slot name="body">
             <pre>{{JSON.stringify(this.paymentData, undefined, 2)}}</pre>
            </slot>
          </div>

          <div class="modal-footer">
            <slot name="footer">
              <button class="modal-default-button" @click="$emit('close')">
                OK
              </button>
            </slot>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
 props: {
  paymentData: {type: Object}
 }
}
</script>


<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, .5);
  display: table;
  transition: opacity .3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 300px;
  margin: 0px auto;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
  transition: all .3s ease;
  font-family: Helvetica, Arial, sans-serif;
}
.modal-header {
  background-color: #62b2eb;
}

.modal-header p {
  margin-top: 0;
  color: white !important;
  padding: 15px;
  font-size: 18px !important;
  font-weight: 700 !important;
  font-family: Noto Sans,Helvetica Neue,Helvetica,Arial,sans-serif;
}

.modal-body {
  margin: 20px 0;
  padding: 20px 30px;
  text-align: left !important;
}

.modal-default-button {
  float: right;
  background-color: #1580dd;
  border-color: #1580dd;
  border-radius: 4px;
  color: white;
  width: 160px;
  font-weight: 400;
  text-align: center;
  cursor: pointer;
  padding: 6px 12px;
  font-size: 14px;
}
.modal-default-button:hover {
  background-color: #1165ae;
  border-color: #1165ae;
}

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-footer {
  height: 30px;
  padding: 20px 30px;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>
