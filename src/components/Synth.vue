<template>
  <q-card class="synth-panel" dark flat bordered>
    <q-card-section class="flex justify-between">
      <div class="q-gutter-md">
        <q-knob
          v-model="synth.envelope.attack"
          :min="0"
          :max="0.1"
          :step="0.001"
          show-value
          color="grey-3"
          center-color="orange"
          track-color="orange"
          >A</q-knob
        >
        <q-knob
          v-model="synth.envelope.decay"
          :min="0"
          :max="1"
          :step="0.01"
          show-value
          color="grey-3"
          center-color="orange"
          track-color="orange"
          >D</q-knob
        >
        <q-knob
          v-model="synth.filterEnvelope.baseFrequency"
          :min="100"
          :max="10000"
          :step="10"
          show-value
          color="grey-3"
          center-color="orange"
          track-color="orange"
          >F</q-knob
        >
      </div>
      <div class="text-h6">{{ name }}</div>
      <div class="q-gutter-md">
        <q-btn
          @mousedown="powerButton()"
          v-bind:class="{ on: isActive, off: !isActive }"
          :ripple="false"
          round
          icon="power_settings_new"
        />
      </div>
    </q-card-section>

    <q-separator inset dark />

    <q-card-section>
      <div class="row">
        <div class="col-2">
          <q-btn
            label="1/4"
            @mousedown="notelen = '4n'"
            v-bind:class="{
              'note-length-active': notelen === '4n',
              'note-length': notelen !== '4n'
            }"
            :ripple="false"
            class="third-button"
            icon="music_note"
            stack
          />
          <q-btn
            label="1/8"
            @mousedown="notelen = '8n'"
            v-bind:class="{
              'note-length-active': notelen === '8n',
              'note-length': notelen !== '8n'
            }"
            :ripple="false"
            class="third-button"
            icon="music_note"
            stack
          />
          <q-btn
            label="1/16"
            @mousedown="notelen = '16n'"
            v-bind:class="{
              'note-length-active': notelen === '16n',
              'note-length': notelen !== '16n'
            }"
            :ripple="false"
            class="third-button"
            icon="music_note"
            stack
          />
        </div>

        <div class="col-2">
          <q-btn
            label="1/4T"
            @mousedown="notelen = '4t'"
            v-bind:class="{
              'note-length-active': notelen === '4t',
              'note-length': notelen !== '4t'
            }"
            :ripple="false"
            class="third-button"
            icon="music_note"
            stack
          />
          <q-btn
            label="1/8T"
            @mousedown="notelen = '8t'"
            v-bind:class="{
              'note-length-active': notelen === '8t',
              'note-length': notelen !== '8t'
            }"
            :ripple="false"
            class="third-button"
            icon="music_note"
            stack
          />
          <q-btn
            label="1/16T"
            @mousedown="notelen = '16t'"
            v-bind:class="{
              'note-length-active': notelen === '16t',
              'note-length': notelen !== '16t'
            }"
            :ripple="false"
            class="third-button"
            icon="music_note"
            stack
          />
        </div>

        <div class="col-3">
          <q-btn
            label="scale 1"
            @mousedown="scale = 1"
            v-bind:class="{
              'sequence-active': scale === 1,
              sequence: scale !== 1
            }"
            class="third-button"
            :ripple="false"
            icon="stairs"
            stack
          />
          <q-btn
            label="scale 2"
            @mousedown="scale = 2"
            v-bind:class="{
              'sequence-active': scale === 2,
              sequence: scale !== 2
            }"
            class="third-button"
            :ripple="false"
            icon="stairs"
            stack
          />
          <q-btn
            label="scale 3"
            @mousedown="scale = 3"
            v-bind:class="{
              'sequence-active': scale === 3,
              sequence: scale !== 3
            }"
            class="third-button"
            :ripple="false"
            icon="stairs"
            stack
          />
        </div>

        <div class="col-3">
          <q-btn
            label="seq 1"
            @mousedown="sequence = 1"
            v-bind:class="{
              'sequence-active': sequence === 1,
              sequence: sequence !== 1
            }"
            class="third-button"
            :ripple="false"
            icon="loop"
            stack
          />
          <q-btn
            label="seq 2"
            @mousedown="sequence = 2"
            v-bind:class="{
              'sequence-active': sequence === 2,
              sequence: sequence !== 2
            }"
            class="third-button"
            :ripple="false"
            icon="loop"
            stack
          />
          <q-btn
            label="seq 3"
            @mousedown="sequence = 3"
            v-bind:class="{
              'sequence-active': sequence === 3,
              sequence: sequence !== 3
            }"
            class="third-button"
            :ripple="false"
            icon="loop"
            stack
          />
        </div>

        <div class="col-2">
          <q-btn
            icon="add"
            @mousedown="octave = 1"
            v-bind:class="{
              'octave-active': octave === 1,
              octave: octave !== 1
            }"
            class="third-button"
            :ripple="false"
          />
          <q-btn
            icon="exposure_zero"
            @mousedown="octave = 0"
            v-bind:class="{
              'octave-active': octave === 0,
              octave: octave !== 0
            }"
            class="third-button"
            :ripple="false"
          />
          <q-btn
            icon="remove"
            @mousedown="octave = -1"
            v-bind:class="{
              'octave-active': octave === -1,
              octave: octave !== -1
            }"
            class="third-button"
            :ripple="false"
          />
        </div>
      </div>
      <div class="row">
        <q-list dense class="col-12">
          <q-item>
            <q-item-section side><q-icon name="volume_up"/></q-item-section>
            <q-item-section>
              <q-slider
                v-model="synth.volume.value"
                :min="-30"
                :max="0"
                color="teal"
              />
            </q-item-section>
          </q-item>
        </q-list>
      </div>
    </q-card-section>
  </q-card>
</template>

<script>
import * as Tone from "tone";
// import * as StartAudioContext from 'startaudiocontext'

export default {
  name: "Synth",
  props: [
    "name",
    "Tone" // tone.js instance
  ],
  data: () => ({
    isActive: false,

    scale: 1,
    sequence: 1,
    notelen: "8n",
    octave: 0,

    synth: new Tone.MonoSynth().toDestination()
    // synth: null
  }),
  created() {
    // this.synth = new Tone.MonoSynth().toDestination()

    console.log(this.Tone);
    console.log(this.synth);

    // The audio context must be started from a user interaction.
    // The following function call takes care of this by starting the audio
    // context with the first user interaction inside the document body.
    // StartAudioContext(Tone.context)

    this.synth.envelope.sustain = 0;
    this.synth.filterEnvelope.octaves = 0;

    const freq = 440;
    const loop = new Tone.Loop(
      time => this.synth.triggerAttack(freq, time),
      this.notelen
    );
    loop.start(Tone.now());

    Tone.start();
  },
  methods: {
    powerButton(index) {
      this.isActive = !this.isActive;
      // this.$emit('playNote', freq)

      // const arpeggio = new Tone.Pattern(
      //   (time, note) => {},
      //   ['C2', 'D4', 'E5', 'A6'],
      //   'upDown'
      // )

      // arpeggio.start(Tone.now())
      // Tone.start()

      // Tone.Transport.start()
      if (this.isActive) {
        Tone.Transport.start();
        // loop.start(Tone.now())
      } else {
        Tone.Transport.pause();
        // loop.pause()
      }
    }
  }
};
</script>

<style lang="scss" scoped>
$scale-color: $orange;
$seq-color: $primary;
$note-color: $teal;
$octave-color: $green;

$scale-color-inactive: change-color($scale-color, $alpha: 0.3);
$seq-color-inactive: change-color($seq-color, $alpha: 0.3);
$note-color-inactive: change-color($note-color, $alpha: 0.3);
$octave-color-inactive: change-color($octave-color, $alpha: 0.3);

.synth-panel {
  width: 100%;
  max-width: 500px;
  height: 325px;
  background-color: $grey-9;
}

.third-button {
  width: 90%;
  height: 50px;
  margin-bottom: 10px;
}

.scale {
  color: $grey-1;
  background-color: $scale-color-inactive;
}

.scale-active {
  color: $grey-1;
  background-color: $scale-color;
}

.sequence {
  color: $grey-1;
  background-color: $seq-color-inactive;
}

.sequence-active {
  color: $grey-1;
  background-color: $seq-color;
}

.note-length {
  color: $grey-1;
  background-color: $note-color-inactive;
}

.note-length-active {
  color: $grey-1;
  background-color: $note-color;
}

.octave {
  color: $grey-1;
  background-color: $octave-color-inactive;
}

.octave-active {
  color: $grey-1;
  background-color: $octave-color;
}

.on {
  color: $grey-1;
  background-color: $teal;
}

.off {
  color: $grey-9;
  background-color: $teal;
}
</style>
