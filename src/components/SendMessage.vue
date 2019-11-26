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
        
        <ChatVote :socket="socket" :toVoteID1="toVoteID1" :toVoteMsg1="toVoteMsg1" :toVoteID2="toVoteID2" :toVoteMsg2="toVoteMsg2"/>

        <v-divider></v-divider>

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
      if(msg && !this.toVoteID1){
        this.toVoteID1 = msg.userID
        this.toVoteMsg1 = msg.text
      }else if(msg && this.toVoteID1) {
        this.toVoteID2 = msg.userID
        this.toVoteMsg2 = msg.text
        document.getElementById("WaitMessage").hidden = true
        document.getElementById("VoteMessage1").hidden = false
        document.getElementById("VoteMessage2").hidden = false
        this.countDown = 10
        this.bar.value = 100
        this.countDownTimer()
      }else if(!msg && this.toVoteID1){
        document.getElementById("WaitMessage").hidden = true
        document.getElementById("VoteMessage1").hidden = false
        document.getElementById("VoteMessage2").hidden = true
        this.countDown = 10
        this.bar.value = 100
        this.countDownTimer()
      } else {
        setTimeout(() => {
          this.socket.emit("request vote")
          this.socket.emit("request vote")
        }, 5000)
      }
    })
    
    setTimeout(() => {
      this.socket.emit("request vote")
      this.socket.emit("request vote")
    }, 10000)
  },
  data: function () {
    return {
      isTargetViewer: true,
      message: '',
      countDown : 0,
      bar:{value:0},
      toVoteID1: null,
      toVoteMsg1: null,
      toVoteID2: null,
      toVoteMsg2: null,
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
        document.getElementById("VoteMessage1").hidden = true
        document.getElementById("VoteMessage2").hidden = true
        document.getElementById("WaitMessage").hidden = false

        // send response
        this.socket.emit("vote response", {userID: this.toVoteID1, isUpvoted: false})
        if(this.toVoteID2 > 1)
          this.socket.emit("vote response", {userID: this.toVoteID2, isUpvoted: false})
        this.toVoteID1 = null
        this.toVoteMsg1 = null
        this.toVoteID2 = null
        this.toVoteMsg2 = null
        setTimeout(() => {
          this.socket.emit("request vote")
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
      console.log("TEMP: Send a message")
    },
  }
}
//<ChatVote :socket="socket" :toVoteMessage="toVoteMessage" :toVoteUserID="toVoteUserID" :countDown="countDown"/>
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


