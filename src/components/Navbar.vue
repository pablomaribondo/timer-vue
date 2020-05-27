<template>
  <nav>
    <v-app-bar app dark class="secondary">
      <v-app-bar-nav-icon @click="isDrawerOpen = !isDrawerOpen" />
      <v-toolbar-title class="headline text-uppercase">
        <span class="font-weight-black primary--text">Vue.js</span>
        <span class="font-weight-light">Timer</span>
      </v-toolbar-title>
    </v-app-bar>

    <v-navigation-drawer app dark v-model="isDrawerOpen">
      <v-toolbar class="secondary">
        <v-toolbar-title class="title">Laps</v-toolbar-title>
      </v-toolbar>
      <v-list>
        <v-list-item
          v-for="(lap, index) in laps"
          :key="index"
        >Lap {{index + 1}}: {{lap.formattedTime}}</v-list-item>
      </v-list>
    </v-navigation-drawer>
  </nav>
</template>

<script>
export default {
  name: "Navbar",
  props: ["laps"],
  data: () => ({
    isDrawerOpen: false
  })
};
</script>

<style>
</style>