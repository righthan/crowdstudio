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


      </v-card>
    </v-col>
  </v-row>
  
</template>

<script>
import ChatVote from '../components/ChatVote.vue'

export default {
  
  name: 'SendMessage',
  components: {ChatVote},
  methods:{
    countDownTimer() {
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
                
            }
  },
  data() {
            return {
                countDown : 10,
                bar:{value:100}
            }
        },

  created() {
           this.countDownTimer()
        },
  
  mounted(){
      this.timer = setInterval(() => {
        this.bar.value = this.bar.value - 10
      }, 1000)

  }
      
}
</script>

<style>
.v-card--reveal {
  align-items: center;
  bottom: 0;
  justify-content: center;
  opacity: .8;
  position: absolute;
  width: 100%;
}


</style>