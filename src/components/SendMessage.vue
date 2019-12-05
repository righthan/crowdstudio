<template>
  <v-card
    class="pa-2"
    tile
    outlined
  >
    <span v-html="usrMessage"/>
    <v-textarea
      v-model="message"
      append-outer-icon='mdi-send'
      @click:append-outer="sendMessage"
      @keydown="OnKeypress"
      autofocus
      label="Shift+Enter will add a new line"
      outlined
      filled
      :background-color="backgroundColor"
      :rules="rules"
      hide-details
      color="purple"
      rows="3"
    />

  </v-card>
  
</template>

<script>

export default {
  name: 'SendMessage',
  props: ["socket"],
  data: function () {
    return {
      rules: [v => v.length >= 1 || 'At least 1 character'],
      isTargetViewer: true,
      usrMessage: "> All viewers (Press <strong>tab</strong> to send to streamer)",
      specialMessageAvialable: true,
      backgroundColor: 'grey lighten-2',
      message: '',
    }
  },

  methods: {
    switchTargetViewer: function () {
      if (this.isTargetViewer) {
        this.usrMessage = "> <span style='color:purple'> <strong>Streamer</strong> </span> (Press <strong>tab</strong> to send to all viewers)"
        this.backgroundColor = '#F3E5F5'
      }
      else {
        this.usrMessage = "> All viewers (Press <strong>tab</strong> to send to streamer)"
        this.backgroundColor = 'grey lighten-2'
      }
      this.isTargetViewer = !this.isTargetViewer
    },
    OnKeypress: function (event) {
      if (event.key === "Tab" && this.specialMessageAvialable) {
        event.preventDefault()
        this.switchTargetViewer()
      }
      else if (event.key === "Enter" && !event.shiftKey) {
        event.preventDefault()
        setTimeout(() => {
          this.sendMessage()
        }, 1000)
      }
    },

    sendMessage: function () {
      if (this.message.length >= 1) {
        this.socket.emit("message", {text: this.message, isSpecial: !this.isTargetViewer})
        this.message = ''
        this.isTargetViewer = true
        this.usrMessage = "> All viewers (Press <strong>tab</strong> to send to streamer)"
        this.backgroundColor = 'grey lighten-2'
      }
    },
  },

  mounted() {
    this.socket.on("msg status update", (msg) => {
      this.specialMessageAvialable = (msg === null)
    })
  }
}
</script>

<style scoped>
.v-card--reveal {
  align-items: center;
  bottom: 0;
  justify-content: center;
  opacity: .8;
  position: absolute;
  width: 100%;
}

</style>


