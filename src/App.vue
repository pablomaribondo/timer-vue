<template>
  <v-app>
    <Navbar :laps="laps" />
    <v-content>
      <Timer
        :timer="formattedTime"
        :state="timerState"
        @start="start"
        @lap="lap"
        @pause="pause"
        @stop="stop"
      />
    </v-content>

    <v-snackbar v-model="snackbar" color="info" :timeout="2000">
      New lap - {{this.latestLap}}
      <v-btn dark text @click="snackbar = false">Close</v-btn>
    </v-snackbar>
  </v-app>
</template>

<script>
import Navbar from "@/components/Navbar";
import Timer from "@/components/Timer";

export default {
  name: "App",

  components: {
    Navbar,
    Timer
  },

  data: () => ({
    timerState: "stopped",
    currentTimer: 0,
    formattedTime: "00:00:00",
    ticker: undefined,
    laps: [],
    latestLap: "",
    snackbar: false
  }),

  methods: {
    start() {
      if (this.timerState !== "running") {
        this.tick();
        this.timerState = "running";
      }
    },
    lap() {
      this.snackbar = true;
      this.laps.push({
        seconds: this.currentTimer,
        formattedTime: this.formatTime(this.currentTimer)
      });

      this.latestLap = this.formatTime(this.currentTimer);
      this.currentTimer = 0;
    },
    pause() {
      clearInterval(this.ticker);
      this.timerState = "paused";
    },
    stop() {
      clearInterval(this.ticker);
      this.timerState = "stopped";
      this.currentTimer = 0;
      this.formattedTime = "00:00:00";
    },
    tick() {
      this.ticker = setInterval(() => {
        this.currentTimer++;
        this.formattedTime = this.formatTime(this.currentTimer);
      }, 1000);
    },
    formatTime(seconds) {
      const measuredTime = new Date(null);
      measuredTime.setSeconds(seconds);

      const HMSTime = measuredTime.toISOString().substr(11, 8);

      return HMSTime;
    }
  }
};
</script>
