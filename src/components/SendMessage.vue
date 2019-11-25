<template>
  <v-row>
    <v-col>
      <v-card
        class="pa-2"
        tile
        outlined
        style="height: 200px;"
      >
        {{usrMessage}}
        <v-textarea
          v-model="message"
          append-outer-icon='mdi-send'
          @click:append-outer="sendMessage"
          @keydown="OnKeydown"
          autofocus
          :label="usrMessage"
          outlined
          filled
          rows="3"
        />

      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'SendMessage',
  data: function () {
    return {
      isTargetViewer: true,
      message: '', 
    }
  },

  computed: {
    usrMessage: function () {
      if (this.isTargetViewer === true) {
        return "> All viewers (Press 'tab' to send to streamer)"
      }
      else {
        return "> Streamer (Press 'tab' to send to all viewers)"
      }
    },
  },

  methods: {
    OnKeydown: function (event) {
      if (event.key === "Tab") {
        event.preventDefault()
        this.isTargetViewer = !this.isTargetViewer
      }
      else if (event.key === "Enter" && event.shiftKey) {
        this.sendMessage()
      }
    },
    sendMessage: function () {
      this.message = ''
      console.log("TEMP: Send a message")
    }
  }
}
</script>