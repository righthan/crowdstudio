<template>

    <v-row id="chatbot" class="mt-2 mb-2" justify=center align=center style="height:100px">
        
        <Candidate1 :socket="socket" :toVoteID="toVoteID" :toVoteMsg="toVoteMsg" :liked="liked" @likeSwitch="likeSwitch()"/>

        <div id="WaitMessage" v-if="!toVoteID">
          Waiting for message(s)...
        </div>
    </v-row>
</template>

<script>
import Candidate1 from '../components/Candidate1.vue'

export default {
  components: {Candidate1},
  props: ["socket", "toVoteID", "toVoteMsg", "liked"],
  name:'ChatVote',
  data() {
        return {
          messageDied: false
        }
    },
  methods: {
    likeSwitch() {
      this.$emit('likeSwitch')
    }
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
