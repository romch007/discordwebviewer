<template>
  <v-container>
    <v-layout row>
      <v-flex>
        <v-card>
          <v-toolbar color="red" dark>
            <v-toolbar-side-icon></v-toolbar-side-icon>

            <v-toolbar-title>Channels</v-toolbar-title>

            <v-spacer></v-spacer>
          </v-toolbar>
          <v-list>
            <v-list-tile
                    v-for="chan in channelsMap.array()"
                    :key="chan.id"
                    avatar
                    @click="clickOnChannel({type: chan.type, id: chan.id})"
            >
              <v-list-tile-action>
                <v-icon v-if="chan.type === 'voice'">keyboard_voice</v-icon>
                <v-icon v-if="chan.type === 'text'">chat</v-icon>
                <v-icon v-if="chan.type === 'category'">label</v-icon>
              </v-list-tile-action>

              <v-list-tile-content>
                <v-list-tile-title v-text="chan.name"></v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
          </v-list>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    name: "Channels",
    props: ["guild", "guildSelected"],
    data() {
      return {
        channelsMap: null
      }
    },
    methods: {
      getChannels() {
        this.channelsMap = this.guild.channels;
      },
      clickOnChannel(chan) {
        if (chan.type === 'text') {
          this.$emit("clickchannel",{
            id: chan.id
          });
        }
      }
    },
    watch: {
      guildSelected(newValue) {
        if (newValue) {
          this.getChannels();
        }
      },
      guild() {
        this.getChannels();
      }
    }
  }
</script>

<style scoped>

</style>