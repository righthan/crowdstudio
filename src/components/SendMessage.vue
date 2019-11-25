<template>
  <v-row>
    <v-col>
      <v-card
        class="pa-2"
        tile
        outlined
        style="height: 220px;"
      >
        Send Message
        {{ countDown }}

          <v-progress-linear :value="bar.value" color="purple"></v-progress-linear>
        
        
        <ChatVote/>

        <v-divider :inset="inset"></v-divider>

        {{usrMessage}}
        <v-textarea
          v-model="message"
          append-outer-icon='mdi-send'
          @click:append-outer="sendMessage"
          @keydown="OnKeydown"
          autofocus
          label="'shift+Enter' will send a message."
          outlined
          filled
          rows="3"
        />

      </v-card>
    </v-col>
  </v-row>
  
</template>

<script>
import ChatVote from '../components/ChatVote.vue'

export default {
  
  name: 'SendMessage',
  components: {
    ChatVote
  },

  created() {
    this.countDownTimer()
  },
  
  mounted() {
    this.timer = setInterval(() => {
      this.bar.value = this.bar.value - 10
    }, 1000)
  },
      
  data: function () {
    return {
      isTargetViewer: true,
      message: '',
      countDown : 10,
      bar:{value:100}
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
    countDownTimer: function () {
      if(this.countDown > 0) {
          setTimeout(() => {
              this.countDown -= 1
              this.countDownTimer()
          }, 1000)
          }
      if(this.countDown==0) {
        var node = document.createElement("div")
        node.setAttribute("id","WaitMessage")
        var textnode = document.createTextNode("Waiting for message...")
        node.appendChild(textnode)
      
        document.getElementById("VoteMessage").remove()
        document.getElementById("Chatbot").appendChild(node)
      }
    },
    OnKeydown: function (event) {
      if (event.key === "Tab") {
        event.preventDefault()
        this.isTargetViewer = !this.isTargetViewer
      }
      else if (event.key === "Enter" && event.shiftKey) {
        event.preventDefault()
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
