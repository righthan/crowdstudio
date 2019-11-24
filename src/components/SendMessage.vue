<template>
  <v-row>
    <v-col>
      <v-card
        class="pa-2"
        tile
        outlined
        style="height: 200px;"
      >
        Send Message
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'SendMessage',
  props: ["socket"],
  methods: {
    sendMessage: function(event) {
      event
      // send message to message variable
      this.socket.emit("message", false)
    }
  }
}
</script>