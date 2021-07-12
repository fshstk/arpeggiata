<template>
  <q-layout view="hhh lpr fff">
    <q-header bordered class="bg-teal text-white">
      <q-toolbar>
        <q-btn
          :ripple="false"
          round
          icon="settings"
          class="settings"
          @click="settingsActive = true"
        />
        <q-icon name="speed" class="q-pl-sm" />
        {{ Math.round(bpm.value) }} BPM

        <!-- TODO: title is not centered -->
        <q-toolbar-title class="text-center">
          Arpeggiata
        </q-toolbar-title>

        <img width="50px" src="~assets/iemlogo.png" />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />

      <q-dialog v-model="settingsActive">
        <settings />
      </q-dialog>
    </q-page-container>

    <q-footer bordered class="q-pa-xs bg-grey-7 text-center">
      <a
        style="text-decoration: none;"
        class="text-white"
        href="https://www.github.com/fshstk"
        >© 2021 Fabian Hummel</a
      >
    </q-footer>
  </q-layout>
</template>

<script>
import * as Tone from "tone";
import Settings from "../components/Settings";

export default {
  name: "MainLayout",
  components: {
    Settings,
  },
  data: () => ({
    bpm: Tone.Transport.bpm,
    settingsActive: false,
  }),
};
</script>

<style lang="scss" scoped>
.settings {
  color: $grey-9;
  background-color: $grey-1;
}
</style>
