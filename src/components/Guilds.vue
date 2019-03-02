<template>
  <v-container>
    <v-layout row>
      <v-flex>
        <v-card>
          <v-toolbar color="indigo" dark>
            <v-toolbar-side-icon></v-toolbar-side-icon>

            <v-toolbar-title>Guilds</v-toolbar-title>

            <v-spacer></v-spacer>
          </v-toolbar>
          <v-list>
            <v-list-tile
                    v-for="guild in guildsCollection.array()"
                    :key="guild.id"
                    avatar
                    @click="goToGuild(guild.id)"
            >
              <v-list-tile-content>
                <v-list-tile-title v-text="guild.name"></v-list-tile-title>
              </v-list-tile-content>

              <v-list-tile-avatar>
                <img alt="icon" :src="guild.iconURL">
              </v-list-tile-avatar>
            </v-list-tile>
          </v-list>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    name: "Guilds",
    props: ["guildsCollection"],
    methods: {
      goToGuild(id) {
        this.$emit("clickguild", {
          guildId: id
        })
      }
    }
  }
</script>

<style scoped>

</style>