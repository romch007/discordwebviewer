<template>
  <v-app>
    <v-content>
      <Connection @validation="connect" :active="isConDialogActive"/>
      <Home :loaded="loaded" :client="client" :v-if="isHomeActive"></Home>
    </v-content>
  </v-app>
</template>

<script>
  import Connection from './components/Connection';
  import Home from './components/Home';
  import Discord from 'discord.js';

  export default {
    name: 'App',
    components: {
      Connection,
      Home
    },
    data() {
      return {
        isConDialogActive: true,
        isHomeActive: false,
        client: new Discord.Client(),
        loaded: false
      }
    },
    methods: {
      connect(data) {
        let token = data.token;
        // Try to log with token
        this.client.login(token)
            .then(() => this.loadHome(token))
            .catch(() => alert("An error has occurred"));
      },
      loadHome(token) {
        this.loaded = true;
        this.isConDialogActive = false;
        this.isHomeActive = true;
        localStorage.setItem("token", token);
      }
    },
    beforeMount() {
      if (localStorage.getItem("token") !== null) {
        this.connect({ token: localStorage.getItem("token") });
      }
    }
  }
</script>
