<template>
  <v-container :v-if="loaded" grid-list-md>
    <h1>Discord Web Viewer</h1>
    <h2>Current user : {{ client.user.username }}#{{ client.user.discriminator }}</h2>
    <v-layout row wrap>
      <v-flex xs6>
        <Guilds
                @clickguild="guildClicked"
                :guilds-collection="guildsCollection"
        ></Guilds>
      </v-flex>
      <v-flex xs6>
        <Channels
                @clickchannel="channelClicked"
                :guild="selectedGuild"
                :guild-selected="isGuildSelected"
                v-if="isGuildSelected"
        ></Channels>
      </v-flex>
    </v-layout>
    <v-flex>
      <Messages
              :channel-selected="isChannelSelected"
              :channel="selectedChannel"
              v-if="isChannelSelected"
      ></Messages>
    </v-flex>
  </v-container>
</template>

<script>
  import Guilds from './Guilds';
  import Channels from './Channels';
  import Messages from './Messages';

  export default {
    components: {
      Guilds,
      Channels,
      Messages
    },
    name: "Home",
    props: {
      client: Object,
      loaded: Boolean
    },
    data() {
      return {
        guildsCollection: null,
        isGuildSelected: false,
        isChannelSelected: false,
        selectedGuild: null,
        selectedChannel: null
      }
    },
    watch: {
      loaded(newValue) {
        if (newValue) {
          this.fetch();
        }
      }
    },
    methods: {
      fetch() {
        this.guildsCollection = this.client.guilds;
      },
      guildClicked(data) {
        this.selectedGuild = this.client.guilds.get(data.guildId);
        this.isGuildSelected = true;
      },
      channelClicked(data) {
        this.selectedChannel = this.selectedGuild.channels.get(data.id);
        this.isChannelSelected = true;
      }
    }
  }
</script>

<style scoped>

</style>