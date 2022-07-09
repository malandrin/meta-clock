<template>
  <div id='app'>
    <div class='numbers'>
      <div class='group'>
        <Number ref='hours_l'/>
        <Number ref='hours_r'/>
      </div>

      <div class='group'>
        <Number ref='minutes_l'/>
        <Number ref='minutes_r'/>
      </div>
    </div>

    <div class='credits'>
      <p>MetaClock By <a href='https://www.cesarbotana.com' target='_blank'>César Botana</a>
      - Source code available at <a href='https://github.com/malandrin/meta-clock' target='_blank'>GitHub</a></p>
    </div>
  </div>
</template>

<script>
import _ from 'lodash';
import Number from './components/number';

export default {
  name: 'App',
  components: {
    Number
  },
  mounted: function() {
    const self = this;

    this.timer = window.setInterval(function() {
      const date = new Date();
      const minutes = date.getMinutes();

      if (minutes !== this.minutes) {
        self.setValue(date.getHours(), 'hours');
        self.setValue(minutes, 'minutes');
        self.minutes = minutes;
      }
    }, 1000);
  },
  beforeDestroy: function() {
    clearInterval(this.timer);
  },
  methods: {
    setValue(val, hand) {
      val = `${val < 10 ? '0' : ''}${val}`;

      this.$refs[`${hand}_l`].setValue(val[0]);
      this.$refs[`${hand}_r`].setValue(val[1]);
    }
  }
}
</script>

<style lang='less' scoped>
  #app {
    margin: 0;
    padding: 0;
    background: #cecece;
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    flex-direction: column;

    .numbers {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100%;

      .group {
        display: flex;
      }
    }

    .credits {
      display: flex;
      align-items: center;
      justify-content: center;
      margin-top: auto;
      margin-bottom: 20px;
    }

    @media screen and (max-width: 767px) {
      .numbers {
        flex-direction: column;
      }
    }
  }
</style>
