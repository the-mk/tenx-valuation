<template>
  <div id="app">
    <div class="uk-container">
      <InfoBoxes></InfoBoxes>
      <form>
        <fieldset class="uk-fieldset">
            <div class="uk-margin uk-grid-small uk-child-width-auto uk-grid">
                <label><input class="uk-checkbox" type="checkbox" v-model="showFormula"> Show Formulas</label>
            </div>
        </fieldset>
    </form>
    <div class="uk-card uk-card-default uk-width-1-2@m">
    <div class="uk-card-header">
        <div class="uk-grid-small uk-flex-middle" uk-grid>
            <div class="uk-width-auto">
            </div>
            <div class="uk-width-expand">
                <h3 class="uk-card-title uk-margin-remove-bottom">TENX valuation</h3>
                <p class="uk-text-meta uk-margin-remove-top"><time datetime="2016-04-01T19:00">Calculator</time></p>
            </div>
        </div>
    </div>
    <div class="uk-card-body">
        <dl class="uk-description-list uk-description-list-divider">
          <dt><b>TENX Circulating Supply</b></dt>
          <dd>105,545,456</dd>
          <dt><b>Revenue distributed <span uk-tooltip="title: Defines an estimate of the percentage from TenX revenue which will be distributed among TENX hodlers; pos: right" uk-icon="icon: info; ratio: 0.65"></span></b></dt>
          <dd>{{ distributedRevenue | formatPercentage }} % </dd><br>
          <form>
              <fieldset class="uk-fieldset">
                  <div class="uk-margin">
                      <input class="uk-range" type="range" min="0" max="2" step="0.05" v-model="distributedRevenue">
                  </div>
              </fieldset>
          </form>
          <dt><b>Unclaimed tokens <span uk-tooltip="title: Defines the percentage of tokens which wont be claimed. Unclaimed tokens will be redistributed among those who claimed; pos: right" uk-icon="icon: info; ratio: 0.65"></span></b></dt>
          <dd>{{ unclaimedAmount | formatPercentage }} %</dd><br>
          <form>
              <fieldset class="uk-fieldset">
                  <div class="uk-margin">
                      <input class="uk-range" type="range" min="20" max="45" step="0.5" v-model="unclaimedAmount">
                  </div>
              </fieldset>
          </form>
      </dl>


    </div>
    <div class="uk-card-footer">
        <a href="#" class="uk-button uk-button-text">Read more</a>
    </div>
</div>
      <div class="uk-card uk-card-default uk-card-body">
          <h3 class="uk-card-title">Unclaimed tokens <span uk-tooltip="title: Defines the percentage of tokens which wont be claimed. Unclaimed tokens will be redistributed among those who claimed; pos: right" uk-icon="icon: info; ratio: 0.65"></span></h3>
          <form>
              <fieldset class="uk-fieldset">
                  <div class="uk-margin">
                      <legend class="uk-legend">{{ unclaimedAmount | formatPercentage }} %</legend>
                      <input class="uk-range" type="range" min="20" max="45" step="0.5" v-model="unclaimedAmount">
                  </div>
              </fieldset>
          </form>
      </div>
      <div class="uk-card uk-card-default uk-card-body">
          <h3 class="uk-card-title">TenX users</h3>
          <form>
              <fieldset class="uk-fieldset">
                  <div class="uk-margin">
                      <legend class="uk-legend">{{ adjustedUserAmount | formatNumber }}</legend>
                      <input class="uk-range" type="range" min="31.632" max="2237" v-model="userAmount">
                  </div>
              </fieldset>
          </form>
      </div>
      <div class="uk-card uk-card-default uk-card-body">
          <h3 class="uk-card-title">Average spending per user per month</h3>
          <form>
              <fieldset class="uk-fieldset">
                  <div class="uk-margin">
                      <legend class="uk-legend">$ {{ spendingUser | formatPercentage }}</legend>
                      <input class="uk-range" type="range" min="5" max="400" step="5" v-model="spendingUser">
                  </div>
              </fieldset>
          </form>
      </div>
      <div class="uk-card uk-card-default uk-card-body">
          <h3 class="uk-card-title">Your PAY at snapshot time</h3>
          <form>
              <fieldset class="uk-fieldset">
                  <div class="uk-margin">
                      <legend class="uk-legend">{{ adjustedAmountPAY | formatNumber }} PAY</legend>
                      <input class="uk-range" type="range" min="3.87298334621" max="500" v-model="amountPAY">
                  </div>
              </fieldset>
          </form>
      </div>
      <div class="uk-card uk-card-secondary uk-card-body">
          <h3 class="uk-card-title">{{ amountTENX | formatNumber }} TENX <span uk-tooltip="title: Estimated amount of TENX tokens you will be able to claim; pos: right" uk-icon="icon: info; ratio: 0.65"></span></h3>
          <p>Your claimable TENX</p> 
          <div v-if="showFormula" class="uk-text-meta">Formula: ( Amount of PAY ) x ( 1 / ( 1 - Revenue distributed ) )</div>
      </div>
      <div class="uk-card uk-card-secondary uk-card-body">
          <h3 class="uk-card-title">$ {{ payoutToken | formatPercentage(4) }}</h3>
          <p>Payout per token per year</p>
          <div v-if="showFormula" class="uk-text-meta">Formula: ( 1 / Circulating TENX ) x ( Revenue distributed x TenX User x Spending per User per month x 12 )</div>
      </div>
      <div class="uk-card uk-card-secondary uk-card-body">
          <h3 class="uk-card-title">$ {{ payoutYear | formatNumber }}</h3>
          <p>Payout per year based on your holdings</p>
          <div v-if="showFormula" class="uk-text-meta">Formula: TENX Holdings x Payout per token per year</div>
      </div>
    </div>
  </div>
</template>

<script>
import InfoBoxes from './components/InfoBoxes.vue';

export default {
  name: 'app', 
  components: {
    InfoBoxes,
  },
  data () {
    return {
      circulatingPAY: 114347861,
      unclaimedAmount: 23,
      distributedRevenue: 0.5,
      spendingUser: 100,
      userAmount: Math.pow(100000, 1/2),
      amountPAY: Math.pow(2500, 1/2),
      showFormula: false
    }
  },
  filters: {
    formatPercentage(value, amount = 2) {
      return parseFloat(value).toFixed(amount);
    },
    formatNumber(value) {
      return parseInt(value).toLocaleString('en');
    }
  },
  computed: {
    amountTENX () {
      return this.adjustedAmountPAY*(1/(1-(this.unclaimedAmount/100)))
    },
    payoutToken () {
      return (1/this.circulatingPAY)*(this.distributedRevenue/100)*this.adjustedUserAmount*this.spendingUser*12
    },
    payoutYear () {
      return this.payoutToken*this.amountTENX
    },
    adjustedAmountPAY () {
      return Math.pow(this.amountPAY, 2)
    },
    adjustedUserAmount () {
      return Math.pow(this.userAmount, 2)
    }
  }
}
</script>

<style>

</style>
