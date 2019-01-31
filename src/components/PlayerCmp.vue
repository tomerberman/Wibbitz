<template>
  <div id="player-container">
    <div id="player-screen">
      <sc0-el0 v-if="this.timePassed > 100 && timePassed < 5100"/>
      <sc0-el1 v-if="this.timePassed > 0 && timePassed < 5100"/>
      <sc0-el2 v-if="this.timePassed > 3000 && timePassed < 5000"/>
      <sc1-el0 v-if="this.timePassed > 5100 && timePassed < 7100"/>
      <sc2-el1 v-if="this.timePassed > 7100 && timePassed < 11000"/>
    </div>
    <player-control :currTime = "timePassed"></player-control>
  </div>
</template>


<script>
import eventBus, {
  START_PLAY,
  PAUSE_PLAY,
  SLIDER
} from "../services/eventBusService.js";
import PlayerControl from "./PlayerControl";
import Sc0El0 from "./Sc0El0";
import Sc0El1 from "./Sc0El1";
import Sc0El2 from "./Sc0El2";
import Sc1El0 from "./Sc1El0";
import Sc2El1 from "./Sc2El1";

export default {
  name: "PlayerCmp",

  data() {
    return {
      running: false,
      playStartTime: Date.now(),
      timePassed: 0,
      videoCurrTime: 0,
      myInterval: null
    };
  },

  components: {
    PlayerControl,
    Sc0El0,
    Sc0El1,
    Sc0El2,
    Sc1El0,
    Sc2El1
  },

  created() {
    eventBus.$on(START_PLAY, _ => this.startClock());
    eventBus.$on(PAUSE_PLAY, _ => this.pauseClock());
    eventBus.$on(SLIDER, sliderPos => this.updateClock(sliderPos));
  },

  methods: {
    runInterval() {
      this.myInterval = setInterval(this.checkTime, 16);
    },

    startClock() {
      this.playStartTime = Date.now();
      this.running = true;
      this.runInterval();
    },

    pauseClock() {
      this.running = false;
      this.videoCurrTime = this.videoCurrTime + Date.now() - this.playStartTime;
      clearInterval(this.myInterval);
    },

    checkTime() {
      this.timePassed = this.videoCurrTime + Date.now() - this.playStartTime;
    //   console.log("time", this.timePassed);
    },

    updateClock(val) {
        this.timePassed = val;
    }
  }
};
</script>

<style scoped>
#player-container {
  padding: 10px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 880px;
  height: 600px;
  background-color: darkgray;
}

#player-screen {
  position: relative;
  height: 480px;
  width: 848px;
  background-color: #333;
}
</style>
