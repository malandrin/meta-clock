<template>
  <div
    ref='clock'
    class='clock'
  >
    <div class='container'>
      <div
        class='hand'
        v-bind:style="{transform: getHandTransform('hours')}"
      />
      <div
        class='hand'
        v-bind:style="{transform: getHandTransform('minutes')}"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'Clock',
  data: function() {
    return {
      hours: 0,
      minutes: 0
    };
  },
  methods: {
    setTime(hours, minutes) {
      this.hours = hours;
      this.minutes = minutes;
    },
    getHandTransform: function(hand) {
      let deg = 0;

      if (hand === 'hours') {
        deg = this.hours * 30;
      } else {
        deg = this.minutes * 6;
      }

      return `rotateZ(${deg}deg)`;
    }
  }
}
</script>

<style lang='less' scoped>
  .clock {
    position: relative;
    height: calc(100vw / 16);
    width: calc(100vw / 16);

    .container {
      position: absolute;
      top: 5px;
      right: 5px;
      bottom: 5px;
      left: 5px;
      background: #fefefe;
      border-radius: 50%;
      box-shadow: inset 0px 0px 15px -2px #282728;
      box-sizing: border-box;

      .hand {
        background: #282728;
        height: 45%;
        left: 47.5%;
        position: absolute;
        top: 5%;
        transform-origin: 50% 99%;
        width: 7%;
        border-radius: 20%;
        transform: rotateZ(45deg);
        transition: transform 10s;
      }
    }

    @media screen and (max-width: 767px) {
      height: calc(100vh / 13);
      width: calc(100vh / 13);
    }
  }
</style>
