<template>

    <v-row id="chatbot" class="mt-2 mb-2" justify=center align=center style="height:100px">
        
        <Candidate1 :socket="socket" :toVoteID="toVoteID1" :toVoteMsg="toVoteMsg1"/>

        <Candidate2 :socket="socket" :toVoteID="toVoteID2" :toVoteMsg="toVoteMsg2"/>
        <div id="WaitMessage">
          Waiting for message(s)...
        </div>
    </v-row>
</template>

<script>
import Candidate1 from '../components/Candidate1.vue'
import Candidate2 from '../components/Candidate2.vue'

export default {
  components: {Candidate1,Candidate2},
  props: ["socket", "toVoteID1", "toVoteMsg1", "toVoteID2", "toVoteMsg2"],
  name:'ChatVote',
  data() {
        return {
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
