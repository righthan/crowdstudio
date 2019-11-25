<template>
  <v-row>
    <v-col>
      <v-card
        class="pa-2"
        tile
        outlined
        style="height: 220px;"
      >
        Vote for Message: {{ countDown }}

        <v-progress-linear :value="bar.value" color="purple"></v-progress-linear>
        
        
        <ChatVote :socket="socket" :toVoteMessage="toVoteMessage" :toVoteUserID="toVoteUserID" :countDown="countDown"/>

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
  props: ["socket"],
  components: {
    ChatVote
  },
  mounted() {
    this.socket.on("vote message", (msg) => {
      if(msg){
        this.toVoteUserID = msg.userID
        this.toVoteMessage = msg.text
        document.getElementById("VoteMessage").hidden = false
        document.getElementById("WaitMessage").hidden = true
        this.countDown = 10
        this.bar.value = 100
        this.countDownTimer()
      } else {
        setTimeout(() => {
          this.socket.emit("request vote")
        }, 5000)
      }
    })
    
    setTimeout(() => {
      this.socket.emit("request vote")
    }, 10000)
  },
  data: function () {
    return {
      isTargetViewer: true,
      message: '',
      countDown : 0,
      bar:{value:0},
      toVoteUserID: "hello",
      toVoteMessage: "hi"
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
              this.bar.value = this.bar.value - 10
              this.countDownTimer()
          }, 1000)
      }
      if(this.countDown==0) {
        document.getElementById("VoteMessage").hidden = true
        document.getElementById("WaitMessage").hidden = false

        // send response
        this.socket.emit("vote response", {userID: this.toVoteUserID, isUpvoted: false})
        this.toVoteUserID = ""
        this.voteMessage = ""
        setTimeout(() => {
          this.socket.emit("request vote")
        }, 5000)
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
      this.socket.emit("message", {text: this.message, isSpecial: !this.isTargetViewer})
      this.message = ''
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
