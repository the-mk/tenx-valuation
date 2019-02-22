<template>
  <div class="uk-card-body">
    <InfoBox v-for="box in boxes" :box="box" :key="box.name"></InfoBox>
  </div>
</template>
<script>
  import InfoBox from './InfoBox.vue';

  export default {
    name: 'InfoBoxes', 
    components: {
      InfoBox,
    },
    data () {
      return {
        boxes: {
          tenxCirculatingSupply: {
            name: 'TENX Circulating Supply',
            type: '',
            hasSlider: false,
            value: 105545456
          },
          revenueDistributed: {
            name: 'Revenue distributed',
            type: ' %',
            hasSlider: true,
            sliderMin: 0,
            sliderMax: 2,
            value: 0.5,
            sliderStep: 0.05,
            hasInfo: 'Defines an estimate of the percentage from TenX revenue which will be distributed among TENX hodlers'
          },
          unclaimedTokens: {
            name: 'Unclaimed Tokens',
            type: ' %',
            hasSlider: true,
            sliderMin: 20,
            sliderMax: 45,
            value: 23,
            sliderStep: 0.5,
            hasInfo: 'Defines the percentage of tokens which wont be claimed. Unclaimed tokens will be redistributed among those who claimed'
          },
          tenxUsers: {
            name: 'TenX Users',
            type: '',
            hasSlider: true,
            sliderMin: 1000,
            sliderMax: 2000000,
            value: 25000,
            sliderStep: 1000

          },
          spendingPerMonth: {
            name: 'Average spending per user per month',
            type: '$',
            hasSlider: true,
            sliderMin: 5,
            sliderMax: 400,
            value: 100,
            sliderStep: 5
          },
          payAmount: {
            name: 'Your PAY amount at snapshot time',
            type: ' PAY',
            hasSlider: true,
            sliderMin: 0,
            sliderMax: 100000,
            value: 2500,
            sliderStep: 250
          },
          claimableTenx: {
            name: 'Your claimable TENX',
            type: ' TENX',
            hasSlider: false,
            isEditable: false,
            hasInfo: 'Estimated amount of TENX tokens you will be able to claim'
          },
          payoutPerYear: {
            name: 'Payout per token per year',
            type: '$',
            hasSlider: false,
            isEditable: false
          },
          totalPayout: {
            name: 'Payout per year based on your holdings',
            type: '$',
            hasSlider: false,
            isEditable: false
          }
        }
      }
    }
  }
</script>