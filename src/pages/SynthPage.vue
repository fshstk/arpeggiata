<template>
  <q-page class="flex flex-center bg-grey-6">
    <div class="q-pa-md items-center">
      <div class="row">
        <div class="col-12 col-md q-pa-xs flex flex-center">
          <Synth name="synth 1" />
        </div>
        <div class="col-12 col-md q-pa-xs flex flex-center">
          <Synth name="synth 2" />
        </div>
      </div>

      <div class="row">
        <div class="col-12 col-md q-pa-xs flex flex-center">
          <Synth name="synth 3" />
        </div>
        <div class="col-12 col-md q-pa-xs flex flex-center">
          <Synth name="synth 4" />
        </div>
      </div>

      <div class="row flex flex-center q-gutter-md q-pa-md">
        <q-btn
          @click="stop()"
          :ripple="false"
          round
          color="orange"
          size="30px"
          icon="stop"
        />
        <q-btn
          @click="togglePlayPause()"
          :ripple="false"
          round
          color="teal"
          size="30px"
          :icon="isPlaying ? 'pause' : 'play_arrow'"
        />
      </div>
    </div>
  </q-page>
</template>

<script>
import Synth from "../components/Synth";
import * as Tone from "tone";
import * as StartAudioContext from "startaudiocontext";

export default {
  name: "SynthPage",
  components: {
    Synth
  },
  data: () => ({
    Tone: Tone,
    isPlaying: false,
    bpm: 120
  }),
  created() {
    // The audio context must be started from a user interaction.
    // The following function call takes care of this by starting the audio
    // context with the first user interaction inside the document body.
    StartAudioContext(this.Tone.context);
  },
  methods: {
    play() {
      this.isPlaying = true;
      this.Tone.Transport.start();
    },
    pause() {
      this.isPlaying = false;
      this.Tone.Transport.pause();
    },
    togglePlayPause() {
      if (this.isPlaying) this.pause();
      else this.play();
    },
    stop() {
      this.isPlaying = false;
      this.Tone.Transport.stop();

      // TODO: resetting transport to 0 works, but loop continues anyway...
      this.Tone.Transport.seconds = 0;
    }
  }
};
</script>

<style lang="scss" scoped></style>
