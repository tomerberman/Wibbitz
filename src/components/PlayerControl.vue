 <template>
  <div id="player-controls">
    <button @click="startPlay">Play</button>
    <div id="seek-bar">SEEEEK</div>
    <button @click="pausePlay">Pause</button>
  </div>
</template>


<script>
import eventBus, {
  START_PLAY,
  PAUSE_PLAY
} from "../services/eventBusService.js";

export default {
  name: "PlayerControl",
  components: {},

  methods: {
    startPlay() {
      console.log("button play");
      eventBus.$emit(START_PLAY);
    },

    pausePlay() {
      console.log("button pause");
      eventBus.$emit(PAUSE_PLAY);
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
  border-radius: 5px;
}

#seek-bar {
  display: inline-block;
}
</style>