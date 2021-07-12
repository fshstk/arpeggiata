<template>
  <q-card class="synth-panel" flat>
    <q-flashcard style="width: 500px;" no-hover>
      <div class="synth-panel">
        <q-flashcard-section
          class="synth-panel-front"
          transition="slide-up-out"
          :active="settingsOpen"
        >
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
                :class="isActive ? 'on' : 'off'"
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
                  @mousedown="arpeggio.interval = getInterval(1 / 4)"
                  :class="
                    arpeggio.interval === getInterval(1 / 4)
                      ? 'note-length-active'
                      : 'note-length'
                  "
                  :ripple="false"
                  class="third-button"
                  icon="music_note"
                  stack
                />
                <q-btn
                  label="1/8"
                  @mousedown="arpeggio.interval = getInterval(1 / 8)"
                  :class="
                    arpeggio.interval === getInterval(1 / 8)
                      ? 'note-length-active'
                      : 'note-length'
                  "
                  :ripple="false"
                  class="third-button"
                  icon="music_note"
                  stack
                />
                <q-btn
                  label="1/16"
                  @mousedown="arpeggio.interval = getInterval(1 / 16)"
                  :class="
                    arpeggio.interval === getInterval(1 / 16)
                      ? 'note-length-active'
                      : 'note-length'
                  "
                  :ripple="false"
                  class="third-button"
                  icon="music_note"
                  stack
                />
              </div>

              <div class="col-2">
                <q-btn
                  label="1/4T"
                  @mousedown="arpeggio.interval = getInterval(1 / 3)"
                  :class="
                    arpeggio.interval === getInterval(1 / 3)
                      ? 'note-length-active'
                      : 'note-length'
                  "
                  :ripple="false"
                  class="third-button"
                  icon="music_note"
                  stack
                />
                <q-btn
                  label="1/8T"
                  @mousedown="arpeggio.interval = getInterval(1 / 6)"
                  :class="
                    arpeggio.interval === getInterval(1 / 6)
                      ? 'note-length-active'
                      : 'note-length'
                  "
                  :ripple="false"
                  class="third-button"
                  icon="music_note"
                  stack
                />
                <q-btn
                  label="1/16T"
                  @mousedown="arpeggio.interval = getInterval(1 / 12)"
                  :class="
                    arpeggio.interval === getInterval(1 / 12)
                      ? 'note-length-active'
                      : 'note-length'
                  "
                  :ripple="false"
                  class="third-button"
                  icon="music_note"
                  stack
                />
              </div>

              <div class="col-3">
                <q-btn
                  :label="$q.screen.gt.xs ? 'scale 1' : void 0"
                  @mousedown="changeScale(0)"
                  :class="scaleIndex === 0 ? 'sequence-active' : 'sequence'"
                  class="third-button"
                  :ripple="false"
                  icon="stairs"
                  stack
                />
                <q-btn
                  :label="$q.screen.gt.xs ? 'scale 2' : void 0"
                  @mousedown="changeScale(1)"
                  :class="scaleIndex === 1 ? 'sequence-active' : 'sequence'"
                  class="third-button"
                  :ripple="false"
                  icon="stairs"
                  stack
                />
                <q-btn
                  :label="$q.screen.gt.xs ? 'scale 3' : void 0"
                  @mousedown="changeScale(2)"
                  :class="scaleIndex === 2 ? 'sequence-active' : 'sequence'"
                  class="third-button"
                  :ripple="false"
                  icon="stairs"
                  stack
                />
              </div>

              <div class="col-3">
                <q-btn
                  :label="$q.screen.gt.xs ? 'seq 1' : void 0"
                  @mousedown="changeSequence(0)"
                  :class="sequenceIndex === 0 ? 'sequence-active' : 'sequence'"
                  class="third-button"
                  :ripple="false"
                  icon="loop"
                  stack
                />
                <q-btn
                  :label="$q.screen.gt.xs ? 'seq 2' : void 0"
                  @mousedown="changeSequence(1)"
                  :class="sequenceIndex === 1 ? 'sequence-active' : 'sequence'"
                  class="third-button"
                  :ripple="false"
                  icon="loop"
                  stack
                />
                <q-btn
                  :label="$q.screen.gt.xs ? 'seq 3' : void 0"
                  @mousedown="changeSequence(2)"
                  :class="sequenceIndex === 2 ? 'sequence-active' : 'sequence'"
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
                  :class="octave === 1 ? 'octave-active' : 'octave'"
                  class="third-button"
                  :ripple="false"
                />
                <q-btn
                  icon="exposure_zero"
                  @mousedown="octave = 0"
                  :class="octave === 0 ? 'octave-active' : 'octave'"
                  class="third-button"
                  :ripple="false"
                />
                <q-btn
                  icon="remove"
                  @mousedown="octave = -1"
                  :class="octave === -1 ? 'octave-active' : 'octave'"
                  class="third-button"
                  :ripple="false"
                />
              </div>
            </div>
            <div class="row">
              <q-list dense class="col-12">
                <q-item>
                  <q-item-section side
                    ><q-icon name="volume_up"
                  /></q-item-section>
                  <q-item-section>
                    <q-slider
                      v-model="synth.volume.value"
                      :min="-30"
                      :max="-6"
                      color="teal"
                    />
                  </q-item-section>
                  <q-item-section side>
                    <q-btn
                      @click="settingsOpen = true"
                      :ripple="false"
                      round
                      icon="settings"
                      class="open-settings"
                      size="sm"
                    />
                  </q-item-section>
                </q-item>
              </q-list>
            </div>
          </q-card-section>
        </q-flashcard-section>

        <q-flashcard-section
          class="synth-panel-back"
          transition="slide-up-in"
          :active="settingsOpen"
        >
          <q-card-section class="flex justify-between">
            <div class="text-h6">{{ name }} settings page</div>
            <div class="q-gutter-md">
              <q-btn
                @click="settingsOpen = false"
                :ripple="false"
                round
                icon="close"
                class="close-settings"
                size="sm"
              />
            </div>
          </q-card-section>
        </q-flashcard-section>
      </div>
    </q-flashcard>
  </q-card>
</template>

<script>
// Importing QVueGlobals is not functionally necessary -- the app compiles and
// runs just fine without it -- but Vetur shows "$q" as an error without it.
import QVueGlobals from "quasar";

import * as Tone from "tone";
import SynthData from "../SynthData";

export default {
  name: "Synth",
  props: ["name"],
  data: () => ({
    settingsOpen: false,
    isActive: false,

    scaleIndex: 0,
    sequenceIndex: 0,
    octave: 0,

    synth: new Tone.MonoSynth().toDestination(),
    arpeggio: null, // initialized in created()
  }),
  created() {
    this.arpeggio = new Tone.Pattern(
      (time, note) => this.synth.triggerAttack(note * 2 ** this.octave, time),
      [], // empty array for now, we will set this using updateScaleSequence()
      "up"
    );

    this.synth.volume.value = -12;
    this.synth.envelope.sustain = 0;
    this.synth.filterEnvelope.octaves = 0;
    this.synth.filterEnvelope.baseFrequency = 2000;

    this.arpeggio.interval = 1 / 4;
    this.updateScaleSequence();
    this.arpeggio.mute = true;
    this.arpeggio.start(0);
  },
  methods: {
    powerButton() {
      this.isActive = !this.isActive;
      this.arpeggio.mute = !this.isActive;
    },
    changeScale(index = 0) {
      this.scaleIndex = index;
      this.updateScaleSequence();
    },
    changeSequence(index = 0) {
      this.sequenceIndex = index;
      this.updateScaleSequence();
    },
    updateScaleSequence() {
      // (1) Convert all notes to Tone.Frequency() type, so we can do stuff like
      // multiply/divide by 2 to change octave:
      const scale = SynthData.scales[this.scaleIndex].split(",").map(note => Tone.Frequency(note));
      // (2) Map the sequence to its scale, i.e. we want to play the notes in
      // the selected scale, in the order specified by the selected sequence.
      // The scale is indexed starting at 1 and wraps around the end of the scale.
      const sequence = SynthData.sequences[this.sequenceIndex];
      this.arpeggio.values = sequence.split(",").map(i => scale[(i - 1) % scale.length]);
    },
    getInterval(noteVal) {
      // Given a certain BPM, we want the period taken up by a note event with
      // note value noteVal, where noteVal is the fraction of a bar taken up by
      // a note event (e.g. quarter note = 1/4, etc.)
      const bpm = Tone.Transport.bpm.value;
      const quarterNoteDuration = 60 / bpm;
      const barDuration = 4 * quarterNoteDuration;
      return noteVal * barDuration;
    },
  },
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
  background-color: transparent;
}

.synth-panel-front {
  width: 100%;
  max-width: 500px;
  height: 325px;
  color: $grey-3;
  background-color: $grey-9;
}

.synth-panel-back {
  width: 100%;
  min-width: 500px;
  max-width: 500px;
  height: 325px;
  color: $grey-9;
  background-color: $grey-3;
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

.open-settings {
  color: $grey-9;
  background-color: $grey-1;
}

.close-settings {
  color: $grey-1;
  background-color: $grey-9;
}
</style>
