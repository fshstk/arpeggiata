<template>
  <q-card>
    <q-card-section>
      <div class="row no-wrap items-center">
        <div class="col text-h6">Settings</div>
      </div>
    </q-card-section>

    <q-card-section class="q-pt-none">
      <q-input outlined v-model="bpm.value" type="number" label="BPM" />

      <div class="text-subtitle2">Scales</div>
      <q-input outlined v-model="scales[0]" label="scale 1" />
      <q-input outlined v-model="scales[1]" label="scale 2" />
      <q-input outlined v-model="scales[2]" label="scale 3" />

      <div class="text-subtitle2">Sequences</div>
      <q-input outlined v-model="sequences[0]" label="sequence 1" />
      <q-input outlined v-model="sequences[1]" label="sequence 2" />
      <q-input outlined v-model="sequences[2]" label="sequence 3" />
    </q-card-section>

    <q-separator />

    <q-card-actions align="right">
      <q-btn v-close-popup flat color="teal" label="Schließen" />
    </q-card-actions>
  </q-card>
</template>

<script>
import * as Tone from "tone";
import SynthData from "../SynthData";

export default {
  name: "Settings",
  data: () => ({
    scales: SynthData.scales,
    sequences: SynthData.sequences,
    bpm: Tone.Transport.bpm,
  }),
};
</script>
