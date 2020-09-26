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
    test: "",
    bpm: Tone.Transport.bpm,
  }),
};
</script>
