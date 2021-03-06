<template>
  <div id="app">
    <div
      v-if="this.$store.state.LicenseKey.expiring || this.$store.state.LicenseKey.expired"
      class="expire-notification d-flex justify-content-center align-items-center"
    >
      <div v-if="this.$store.state.LicenseKey.expiring">
        License is expiring in {{ this.$store.state.LicenseKey.days }} days. <a
          class="js-external-link renew-link"
          href="https://gum.co/ridereceiptspro"
        >Click here to renew</a>.
      </div>
      <div v-if="this.$store.state.LicenseKey.expired">
        License has expired. <a
          class="js-external-link renew-link"
          href="https://gum.co/ridereceiptspro"
        >Click here to renew</a>.
      </div>
    </div>
    <transition name="fade">
      <router-view />
    </transition>
  </div>
</template>

<script>
import 'bootstrap-vue/dist/bootstrap-vue.css'
import jetpack from 'fs-jetpack'

export default {
  name: 'Ridereceipts',
  mounted () {
    const documentDir = jetpack.cwd(this.$electron.remote.app.getPath('documents'))

    if (!this.$electronstore.get('invoicePath')) {
      this.$electronstore.set('invoicePath', `${documentDir.path()}/Ride Receipts/`)
    }
  }
}
</script>

<style lang="scss">
@import 'node_modules/bootstrap/scss/bootstrap';
@import url('https://use.fontawesome.com/releases/v5.0.2/css/all.css');
@import url('https://fonts.googleapis.com/css?family=Nunito:400,600,700,800');

$font-family-sans-serif: 'Nunito';
$blue: #0B1E4E;

#app,
html,
body {
  height: 100%;
}

body {
  color: #000;
  font-family: 'Nunito', sans-serif;
  font-size: 1em;
  overflow: hidden;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

a {
  color: #00AFB0;
  text-decoration: none;
  border-bottom: 0;

  &:hover {
    color: #003132;
  }
}

::selection {
  background-color: rgba(0,175,176,0.75);
  color: white;
  text-shadow: none
}

.fade-enter-active, .fade-leave-active {
  transition-duration: 0.2s;
  transition-property: opacity;
  transition-timing-function: ease;
}
.fade-enter, .fade-leave-active {
  opacity: 0
}

.vue-simple-spinner {
  border-color: #00AFB0 rgb(238, 238, 238) rgb(238, 238, 238) !important;
}

.bs-popover-bottom {
  top: 2px !important;
}

.popover .arrow {
  margin: 0.04rem 0.3rem;
}

.bs-popover-bottom .arrow::before, .bs-popover-auto[x-placement^="bottom"] .arrow::before {
  border-bottom-color: rgba(0, 0, 0, 0.10);
}

.bs-popover-bottom .arrow::after, .bs-popover-auto[x-placement^="bottom"] .arrow::after {
  z-index:50000;
}

.popover {
  box-shadow: 0 2px 4px 0 rgba(0,0,0,0.50);
  border: 1px solid #E4E4E4;
  width: 370px;
  max-width: 100%;
  top:30px;
  padding-left: 16px;
  padding-right: 16px;
  padding-bottom: 10px;
  padding-top: 10px;
  border-radius: 0;
  font-weight: 400;
  font-size: 14px;
  font-family: 'Nunito', sans-serif;

  p {
    margin-bottom: 5px;
  }

  p.text-right {
    margin-top: 15px;
    margin-bottom: 5px;
  }

  a {
    font-weight: 800;
    font-size: 12px;
    color: #00afb0;
  }
}

.popover-header {
  padding-top: 20px;
  padding-bottom: 0px;
  font-family: 'Nunito', sans-serif;
  background: none !important;
  border-bottom: 0px;
  font-weight: 800;
  color: black;
}

.sign-in-text {
  font-size: 36px;
  color: #000;
  font-weight:800;
  line-height: 42px;
}

.loading-text {
  font-size: 36px;
  color: #000 !important;
  font-weight:800;
  line-height: 42px;
}

.fa-question-circle {
  color: #898989;
  font-size: 18px;
  top: -10px;
  position: relative;
  cursor: pointer;
}

.btn--submit {
  font-size: 24px;
  right: 10px;
  /* Rounded button: */
  background: #FFFFFF;
  border-radius: 100px;
  height: 52px;
  width: 178px;
  border: 0px;
  font-weight: 800;
  color: black;
  text-transform: uppercase;

  &:active,
  &:hover,
  &:focus {
    color: #000;
    background: #FFFFFF;
  }

  &:hover {
    box-shadow: 1px 1px 4px 2px rgba(160,160,160,0.50);
  }

  .arrow {
    margin-left: 10px;
    top: -1px;
    position:relative;
  }
}

.back-btn {
  left: 50px !important;

  img {
    margin-left: 0 !important;
    margin-right: 10px;
  }
}

.btn-started {
  background: #00AFB0;
  color: white;
  border-radius: 30px;
  width: auto;
  height: 52px;
  padding-left:45px;
  padding-right: 45px;
  text-transform: uppercase;
  font-size: 15px;
  font-weight: 700;

  &:active,
  &:focus,
  &:focus:enabled {
    background: white;
  }

  &:hover,
  &:hover:enabled {
    background: #003132;
    color: white;
  }
}

.contribution-box {
  background :#6000B3;

  p:first-of-type {
    font-size: 18px;
    font-weight: 800;
  }

  p {
    color: #fff;
    font-size: 14px;
  }

  a {
    color: #fff;
    padding-bottom: 1px;
    text-decoration: none;

    &:hover {
      border-bottom: 1px solid #fff;
    }
  }
}

.card {
  border-radius: 0;
  background: #FFFFFF;
  border: 0px;
  box-shadow: 0 2px 4px 1px rgba(0,0,0,0.32);

  .card-body {
    .card-text {
      color: #000;
      font-size: 14px;
    }
    .trip-count {
      font-size: 22px;
      color: #000;
      font-weight: 800;
    }
  }
  .card-footer {
    border: 0px;
  }
}

.progress {
  background-color: #D9D9D9;
  height: 16px;
  border-radius: 1rem;
  // width: 80%;
  // margin: 10px auto;
}

.progress-bar {
  background: linear-gradient(to right, rgba(0,175,176,1) 0%, rgba(0,49,50,1) 100%);
}

/* Loading indicator */
.loading {
  position: relative;
  margin:0 auto;
  width: 62px;    /* diameter */
  height: 62px;    /* diameter */

  .inner,
  &:after {
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
  }
  /* Mask */
  &:after {
    content:" ";
    margin: 10%;    /* stroke width */
    border-radius: 100%;
    background: #fff;    /* container background */
  }
  /* Spinning gradients */
  .inner {
    animation-duration: 1s;    /* speed */
    -webkit-animation-duration: 1s;    /* speed */
    animation-iteration-count: infinite;
    -webkit-animation-iteration-count: infinite;
    animation-timing-function: linear;
    -webkit-animation-timing-function: linear;
    animation-name: rotate-inner;
    -webkit-animation-name: rotate-inner;

    /* Halfs */
    &:before,
    &:after {
      position: absolute;
      top: 0;
      bottom: 0;
      content:" ";
    }
    /* Left half */
    &:before {
      left: 0;
      right: 50%;
      border-radius: 72px 0 0 72px;    /* diameter */
    }
    /* Right half */
    &:after {
      left: 50%;
      right: 0;
      border-radius: 0 72px 72px 0;    /* diameter */
    }
    /* Half gradients */
    &:before {
      background-image: linear-gradient(to bottom, #003132 0%, #00AFB0 100%);
    }
    &:after {
        background-image: linear-gradient(to bottom, #ffffff 0%, #D8D8D8 100%);
    }
  }
}

  .form-check-label {
    display: block;
    margin-bottom: 15px;
    font-size: 24px;
    line-height: 32px;
    color: black;
    padding-left: 15px;
  }

    input[type="radio"] {
      margin-top: 8px;
      margin-left: -30px;
      width: 20px;
      height: 20px;
    }

/* Spinning animations */

@keyframes rotate-inner {
  0% {
    transform: rotate(0deg);
    -moz-transform: rotate(0deg);
    -webkit-transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
    -moz-transform: rotate(360deg);
    -webkit-transform: rotate(360deg);
  }
}
@-webkit-keyframes rotate-inner {
  0% {
    -webkit-transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(360deg);
  }
}

footer {
  height: 140px;
}

.form-control.is-valid {
  border-color: #000;
  color: black;

  &:focus {
    outline: 0;
    box-shadow: none;
  }
}

.form-control:disabled, .form-control[readonly] {
    background-color: #fff;
    opacity: 1;
}

  .form-control {
    padding-left: 0;
    padding-bottom: 8px !important;
    outline: none;
    border: none;
    border-bottom: 2px solid rgba(0, 0, 0, 1);
    background-color: transparent;
    border-radius: 0px;
    padding-bottom: 0;
    font-size: 1.9em;
    color: black;
    caret-color: #00AFB0;
    text-overflow: ellipsis;
    transition: all 0.5s ease;
    margin: 0 auto;

    &:focus {
      border-image:  linear-gradient(to right, rgba(0, 175, 176,1) 0%, rgba(0,49,50,1) 100%);
      border-image-slice: 1;
      box-shadow: none;
      background: none;
      outline: none;
    }
  }

  .invalid-feedback {
    width: 100%;
    margin:10px auto;
  }

  .password-lock {
    position: relative;
      top: -35px;
      bottom: 0;
      left: 96.5%;
  }

    .btn--submit-start {
      font-size: 24px;
      right: 10px;
      /* Rounded button: */
      background: #FFFFFF;
      border-radius: 100px;
      height: 52px;
      padding-left: 20px;
      padding-right: 20px;
      border: 0px;
      font-weight: 800;
      color: black;
      text-transform: uppercase;

      &:active,
      &:focus {
        background: #fff;
      }
      &:hover {
        background: #fff;
        color: #000;
        box-shadow: 1px 1px 4px 2px rgba(160,160,160,0.50);
      }

      .arrow {
        margin-left: 10px;
        top: -1px;
        position:relative;
      }
    }

    .VueCarousel-navigation-next,
    .VueCarousel-navigation-prev {
      margin-left: 10px;
    }

    .VueCarousel-navigation-next {
      margin-right:10px;
    }

    .VueCarousel-pagination {
      display: none;
    }

    .btn-outline-primary:not(:disabled):not(.disabled):active {
      background-color: #fff;
      color: #000;
      border-color: #fff;
    }

    [v-cloak] {
      display: none;
    }

    .col-form-label {
      color: #000;
      font-size: 24px;
    }

    .v2-date-wrap {
      min-width: 250px !important;
      height: auto !important;
      border-color: #898989 !important;
    }

    .v2-picker-trigger {
      line-height: 50px !important;
      padding-left: 45px !important;
      height: auto !important;
      font-size: 24px !important;
      color: #000;
    }

    .v2-date-icon {
      left: 10px;
      right: 0 !important;
    }

    .v2-picker-panel__day.selected span {
      background: #00AFB0 !important;
    }

    .v2-picker-panel__day:hover {
      color: #00AFB0 !important;
    }

    .v2-picker-panel__day.today span {
      color: #00AFB0 !important;
    }

    .v2-picker-panel-wrap {
      top:45% !important;
    }

    .btn-card {
      width: 100%;
      border-radius: 0;
      background-color: #00AFB0;
      color: #fff;
      text-transform: uppercase;
      padding-top: 20px;
      padding-bottom: 20px;
      border:0;
      font-weight: 700;
      outline: 0;
      box-shadow: none;
    }
    .btn-card:hover {
      background-color: #003132;
      color: white;
    }
    .expire-notification {
      height: 40px;
      background: black;
      text-align: center;
      color: #fff;
    }

    .v2-toggle-icon__prev-year:hover::before, .v2-toggle-icon__next-year:hover::before, .v2-toggle-icon__prev-year:hover::after, .v2-toggle-icon__next-year:hover::after {
      border-color: #00afb0 !important;
    }

    .v2-toggle-icon__prev-month:hover::before, .v2-toggle-icon__next-month:hover::before {
      border-color: #00afb0 !important;
    }

    .renew-link {
      color: white;

      &:hover {
        color: #00afb0;
      }
    }
</style>
