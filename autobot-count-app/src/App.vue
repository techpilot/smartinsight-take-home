<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <h1>Autobot Count</h1>
  <p v-if="autobotCount !== null">Current Autobot Count: {{ autobotCount }}</p>
  <p v-else>Loading...</p>
</template>

<script>
import { io } from "socket.io-client";

export default {
  name: "App",
  components: {},
  data() {
    return {
      autobotCount: null,
      socket: null,
    };
  },
  mounted() {
    // Connect to your Socket.IO server
    this.socket = io("http://localhost:3000");
    console.log(this.socket);

    // Listen for the autobotCount event
    this.socket.on("autobotCount", (count) => {
      this.autobotCount = count;
    });
  },
  beforeUnmount() {
    // Clean up the socket connection when the component is destroyed
    if (this.socket) {
      this.socket.disconnect();
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
