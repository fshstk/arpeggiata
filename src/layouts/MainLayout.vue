<template>
  <q-layout view="hhh lpr fff">
    <q-header bordered class="bg-teal text-white">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title class="text-center">
          Arpeggiata
        </q-toolbar-title>

        <img width="50px" src="~assets/iemlogo.png" />
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-1"
    >
      <q-list>
        <q-item-label header class="text-grey-8">
          Essential Links
        </q-item-label>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

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
import EssentialLink from "components/EssentialLink.vue";

const linksData = [
  {
    title: "Project Repository",
    caption: "github.com",
    icon: "engineering",
    link: "https://github.com/fshstk/arpeggiata"
  }
];

export default {
  name: "MainLayout",
  components: {
    EssentialLink
  },
  data: () => ({
    leftDrawerOpen: false,
    essentialLinks: linksData
  })
};
</script>
