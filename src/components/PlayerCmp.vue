<template>
  <div id="player-container">
    <div id="player-screen">
      <sc0-el0 v-if="this.timePassed > 100 && timePassed < 5100"/>
      <sc0-el1 v-if="this.timePassed > 0 && timePassed < 5100"/>
      <sc0-el2 v-if="this.timePassed > 3000 && timePassed < 5000"/>
    </div>
    <player-control></player-control>
  </div>
</template>


<script>
import eventBus, {
  START_PLAY,
  PAUSE_PLAY
} from "../services/eventBusService.js";
import PlayerControl from "./PlayerControl";
import Sc0El0 from "./Sc0El0";
import Sc0El1 from "./Sc0El1";
import Sc0El2 from "./Sc0El2";

export default {
  name: "PlayerCmp",

  data() {
    return {
      running: false,
      playStartTime: Date.now(),
      timePassed: 0,
      videoCurrTime: 0
    };
  },

  components: {
    PlayerControl,
    Sc0El0,
    Sc0El1,
    Sc0El2
  },

  created() {
    eventBus.$on(START_PLAY, _ => this.startClock());
    eventBus.$on(PAUSE_PLAY, _ => (this.running = false));
  },

  methods: {
    runInterval() {
      const myInterval = setInterval(this.checkTime, 16);
    },

    startClock() {
      this.playStartTime = Date.now();
      this.running = true;
      this.runInterval();
    },

    checkTime() {
      this.timePassed = Date.now() - this.playStartTime;
      console.log("time", this.timePassed);
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
