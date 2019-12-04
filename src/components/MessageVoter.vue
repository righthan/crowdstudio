<template>
    <v-card
      class="pa-2 text-center"
      tile
      style="height: 300px;"
    >
        <span class="panel_header_lg">
          Click a message in {{ countDown }}s if you like it. <v-icon color="gray">mdi-thumb-up</v-icon>
        </span>

        <v-progress-linear :value="bar.value" color="purple"></v-progress-linear>
        
        <ChatVote :socket="socket" :toVoteID="toVoteID" :toVoteMsg="toVoteMsg" :liked="liked" @likeSwitch="likeSwitch()"/>
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
      if(msg){
        this.toVoteID = msg.userID
        this.toVoteMsg = msg.text
        this.countDown = 10
        this.bar.value = 100
        this.liked = false
        this.countDownTimer()
      } else {
        setTimeout(() => {
          this.socket.emit("request vote")
        }, 1000)
      }
    })
    
    setTimeout(() => {
      this.socket.emit("request vote")
    }, 10000)
  },
  data: () =>({
    countDown : 0,
    bar:{value:0},
    toVoteID: null,
    toVoteMsg: null,
    liked: false
  }),

  methods: {
    likeSwitch() {
      this.liked = !this.liked
      console.log(this.liked)
    },
    countDownTimer: function () {
      console.log("countdown")
      if(this.countDown > 0) {
          setTimeout(() => {
              this.bar.value = this.bar.value - 1
              if(this.bar.value % 10 == 0)
                this.countDown = this.bar.value / 10
              this.countDownTimer()
          }, 100)
      }else if(this.countDown == 0) {
        // send response
        this.socket.emit("vote response", {userID: this.toVoteID, message: this.toVoteMsg, isUpvoted: this.liked})
        this.toVoteID = null
        this.toVoteMsg = null
        setTimeout(() => {
          this.socket.emit("request vote")
        }, 10000)
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