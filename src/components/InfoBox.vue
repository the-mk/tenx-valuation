<template>
  <dl class="uk-description-list uk-description-list-divider">
    <dt><b>{{ box.name }} <span v-if="box.hasInfo" :uk-tooltip="this.hasInfo" uk-icon="icon: info; ratio: 0.65"></span></b></dt>
    <dd>{{ this.figure }}</dd><br>
    <form v-if="box.hasSlider">
      <fieldset class="uk-fieldset">
        <div class="uk-margin">
          <input class="uk-range" type="range" :min="box.sliderMin" :max="box.sliderMax" :step="box.sliderStep" v-model="box.value">
        </div>
      </fieldset>
    </form>
  </dl>
</template> 

<script>
  export default {
    name: 'InfoBox',
    props: {
      box: Object
    },
    computed: {
      hasInfo () {
        return 'title: ' + this.box.hasInfo + '; pos: right';
      },
      figure () {
        let figure = 0;
        let value = this.box.value;
        if (this.box.type != '') {
          value = parseFloat(value).toFixed(2);
        }
        value = parseFloat(value).toLocaleString('en-EN')
        if (this.box.type.charAt(0) == ' ') {
          figure = value + this.box.type;
        } else {
          figure = this.box.type + value;
        }
        return figure;
      }
    }
  }
</script>