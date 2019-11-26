<template>
    <v-card
      class="pa-2 text-center"
      tile
      style="height: 300px;"
    >
        <span class="panel_header_lg">
          Click a message in {{ countDown }}s if you like it. <v-icon color="blue">mdi-thumb-up</v-icon>
        </span>

        <v-progress-linear :value="bar.value" color="purple"></v-progress-linear>
        
        <ChatVote :socket="socket" :toVoteID1="toVoteID1" :toVoteMsg1="toVoteMsg1" :toVoteID2="toVoteID2" :toVoteMsg2="toVoteMsg2"/>
    </v-card>

</template>

<script>
import ChatVote from '../components/ChatVote.vue'
export default {
  name: 'MessageVoter',
  props: ["socket"],
  components:{
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
        this.countDown = 10
        this.bar.value = 100
        this.countDownTimer()
      }else if(!msg && this.toVoteID1){
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
  data: () =>({
    countDown : 0,
    bar:{value:0},
    toVoteID1: null,
    toVoteMsg1: null,
    toVoteID2: null,
    toVoteMsg2: null,
  }),

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