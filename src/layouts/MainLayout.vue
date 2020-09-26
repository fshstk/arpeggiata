<template>
  <q-layout view="hhh lpr fff">
    <q-header bordered class="bg-teal text-white">
      <q-toolbar>
        <q-btn :ripple="false" round icon="settings" class="settings" />
        <q-icon name="speed" class="q-pl-sm" /> {{ bpm.value }} BPM

        <!-- TODO: title is not centered -->
        <q-toolbar-title class="text-center">
          Arpeggiata
        </q-toolbar-title>

        <img width="50px" src="~assets/iemlogo.png" />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer bordered class="q-pa-xs bg-grey-7 text-center">
      <a
        style="text-decoration: none;"
        class="text-white"
        href="https://www.github.com/fshstk"
        >© 2016 Fabian Hummel</a
      >
    </q-footer>
  </q-layout>
</template>

<script>
import * as Tone from "tone";

export default {
  name: "MainLayout",
  components: {
    //
  },
  data: () => ({
    bpm: Tone.Transport.bpm,
  }),
};
</script>

<style lang="scss" scoped>
.settings {
  color: $grey-9;
  background-color: $grey-1;
}
</style>
