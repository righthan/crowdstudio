<template>
  <v-card
    class="pa-2"
    tile
    outlined
    style="height: 150px;"
  >
    <span v-html="usrMessage"/>
    <v-textarea
      v-model="message"
      append-outer-icon='mdi-send'
      @click:append-outer="sendMessage"
      @keydown="OnKeydown"
      autofocus
      label="Shift+Enter will add a new line"
      outlined
      filled
      :background-color="backgroundColor"
      color="purple"
      rows="3"
    />

  </v-card>
  
</template>

<script>

export default {
  name: 'SendMessage',

  data: function () {
    return {
      isTargetViewer: true,
      usrMessage: "> All viewers (Press <strong>tab</strong> to send to streamer)",
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

    OnKeydown: function (event) {
      if (event.key === "Tab") {
        event.preventDefault()
        this.switchTargetViewer()
      }
      else if (event.key === "Enter" && !event.shiftKey) {
        event.preventDefault()
        this.sendMessage()
      }
    },

    sendMessage: function () {
      this.message = ''
      console.log("TEMP: Send a message")
    },
    reflectLike: function() {
      this.messageLiked = true;
      var node = document.createElement("div")
      node.setAttribute("id","WaitMessage")
      var textnode = document.createTextNode("Waiting for message...")
      node.appendChild(textnode)
    
      document.getElementById("VoteMessage").remove()
      document.getElementById("Chatbot").appendChild(node)
      //alert(this.messageLiked)
      
    }
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
