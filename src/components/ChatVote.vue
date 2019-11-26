<template>

    <v-row id="chatbot" class="mt-2 mb-2" justify=center align=center style="height:100px">
        
        <Candidate1/>

        <Candidate2/>

    </v-row>
</template>

<script>
import Candidate1 from '../components/Candidate1.vue'
import Candidate2 from '../components/Candidate2.vue'

export default {
    components: {Candidate1,Candidate2},

    name:'ChatVote',

    methods:{
    like: function() {
          this.liked = !this.liked;
          this.$emit("clickLike", this.liked, this.rank)
          this.$emit("messageLike");
          },

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

            document.getElementById("VoteMessage1").remove()
            document.getElementById("VoteMessage2").remove()
            document.getElementById("chatbot").appendChild(node)
        }
    },

  },
  data() {
        return {
            countDown : 10,
            messages: {message1:" Message  Message  Message  Message", message2:" Message  Message  Message  Message"},
            liked: false,
        }
    },

  created() {
        this.countDownTimer()
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
