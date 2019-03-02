<template>
  <v-container>
    <v-dialog
            v-model="active"
            width="500"
            persistent
    >
      <v-card>
        <v-card-title
                class="headline grey lighten-2"
                primary-title
        >
          Connection
        </v-card-title>

        <v-card-text>
          Paste your token here
          <v-text-field
                  label="Token"
                  prepend-inner-icon="lock"
                  v-model="tokenText"
          ></v-text-field>
        </v-card-text>




        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
                  color="success"
                  flat
                  @click="submit"
          >
            Connect
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
  export default {
    props: {
      active: Boolean
    },
    data() {
      return {
        tokenText: ""
      }
    },
    methods: {
      submit() {
        this.$emit("validation", {
          token: this.tokenText
        })
      }
    }
  }
</script>

<style>

</style>
