 <template>
  <div id="player-controls">
    <button @click="startPlay">Play</button>
    <div id="slider-container">
      <input
        v-model="sliderValue"
        id="slider"
        @change="readSlider"
        type="range"
        max="11100"
        step="10"
        value="0"
      >
      <!-- <div>Time: {{sliderValue/1000}}</div> -->
      <div>Time: {{currTime/1000}}</div>
    </div>
    <button @click="pausePlay">Pause</button>
  </div>
</template>


<script>
import eventBus, {
  START_PLAY,
  PAUSE_PLAY,
  SLIDER
} from "../services/eventBusService.js";

export default {
  name: "PlayerControl",
  components: {},
  props: ["currTime"],

  data() {
    return {
      sliderValue: 0
    };
  },

  methods: {
    startPlay() {
      console.log("button play");
      eventBus.$emit(START_PLAY);
    },

    pausePlay() {
      console.log("button pause");
      eventBus.$emit(PAUSE_PLAY);
    },

    readSlider() {
      var sliderValue = document.querySelector("#slider").value;
      eventBus.$emit(SLIDER, sliderValue);
      console.log("slider", sliderValue);
    }
  }
};
</script>


<style>
#player-controls {
  display: flex;
  height: 120px;
  justify-content: space-around;
  align-items: center;
  background-color: #ccc;
  width: 400px;
}

button {
  display: inline-block;
  height: 50px;
  width: 80px;
  border-radius: 5px;
}

#seek-bar {
  display: inline-block;
}
</style>