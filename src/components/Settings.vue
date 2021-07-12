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
      <q-input outlined v-model="test" label="scale 1" />
      <q-input outlined v-model="test" label="scale 2" />
      <q-input outlined v-model="test" label="scale 3" />

      <div class="text-subtitle2">Sequences</div>
      <q-input outlined v-model="test" label="sequence 1" />
      <q-input outlined v-model="test" label="sequence 2" />
      <q-input outlined v-model="test" label="sequence 3" />
    </q-card-section>

    <q-separator />

    <q-card-actions align="right">
      <q-btn v-close-popup flat color="teal" label="Speichern" />
    </q-card-actions>
  </q-card>
</template>

<script>
import * as Tone from "tone";

export default {
  name: "Settings",
  data: () => ({
    scales: [
      ["D4", "E4", "F4", "G4", "E4", "E4", "C4", "D4"],
      ["C4", "C4", "C5", "C5", "B4", "G4", "A4", "G4"],
      ["F4", "A4", "B4", "B4", "F4", "A4", "B4", "B4"],
    ],
    sequences: [
      [1, 3, 2, 5, 3, 2],
      [1, 3, 2, 5, 3, 2],
      [1, 3, 2, 5, 3, 2],
    ],
    bpm: Tone.Transport.bpm,
  }),
};
</script>
