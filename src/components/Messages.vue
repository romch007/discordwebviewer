<template>
  <v-container>
    <v-layout row>
      <v-flex>
        <v-card>
          <v-toolbar color="blue" dark>
            <v-toolbar-side-icon></v-toolbar-side-icon>

            <v-toolbar-title>Messages</v-toolbar-title>

            <v-spacer></v-spacer>

            <v-toolbar-items class="hidden-sm-and-down">
              <v-flex>
                <v-text-field
                        label="Limit"
                        outline
                        type="number"
                        min="1"
                        v-model="limit"
                ></v-text-field>
              </v-flex>
            </v-toolbar-items>

            <v-spacer></v-spacer>
          </v-toolbar>

          <v-list>

            <v-list-tile v-for="message in messages" :key="message.id">
              <v-list-tile-avatar>
                <img alt="avatar" :src="message.author.avatarURL">
              </v-list-tile-avatar>

              <v-list-tile-content>
                <v-list-tile-title>{{ message.author.username }}</v-list-tile-title>
                <v-list-tile-sub-title>{{ message.content }}</v-list-tile-sub-title>
              </v-list-tile-content>
            </v-list-tile>
          </v-list>

          <!-- Send form -->

            <v-layout row wrap>
              <v-flex>
                <v-text-field
                        label="Send a message"
                        solo
                        v-model="textInput"
                        @keypress.enter="sendMessage"
                ></v-text-field>
              </v-flex>
              <v-flex>
                <v-btn
                        @click="sendMessage"
                        color="success"
                >Send</v-btn>
              </v-flex>
            </v-layout>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    name: "Messages",
    props: ["channelSelected", "channel"],
    data: function () {
      return {
        messages: [],
        textInput: "",
        limit: 20
      };
    },
    watch: {
      channelSelected(newValue) {
        if (newValue) {
          this.getMessages();
        }
      },
      channel() {
        this.getMessages();
      },
      limit() {
        this.getMessages();
      }
    },
    methods: {
      getMessages() {
        this.channel.fetchMessages({limit: this.limit})
            .then(response => {
              this.messages = response.array().reverse();
            })
      },
      sendMessage() {
        this.channel.send(this.textInput);
        this.textInput = "";
      }
    }
  }
</script>

<style scoped>

</style>