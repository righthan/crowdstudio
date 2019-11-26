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
        
        <ChatVote @messageLike = "reflectLike"/>
    </v-card>

</template>

<script>
import ChatVote from '../components/ChatVote.vue'
export default {
  name: 'MessageVoter',
  components:{
      ChatVote
    },

  created() {
    this.countDownTimer()
  },

  mounted() {
    this.timer = setInterval(() => {
      this.bar.value = this.bar.value - 1
    }, 100)
  },

  data: () =>({
    countDown : 10,
    bar:{value:100},
    messageShow: false,
  }),

  methods:{
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