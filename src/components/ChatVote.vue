<template>

    <v-row class="mt-2 mb-2" justify=center align=center style="height:100px">

            <v-col cols="9" id="Chatbot">
                <v-hover v-slot:default="{ hover }" id="VoteMessage" hidden="true">
                  <v-card color="#F3E5F5">
                    
                    <v-expand-transition>
                      <div
                          @click="LikeMessage()"
                          v-if="hover"
                          class="d-flex transition-fast-in-fast-out white darken-2 v-card--reveal display-3"
                          style="height: 100%; cursor:pointer;"
                      >
                          <v-icon color="deep-purple">mdi-thumb-up</v-icon>
                      </div>
                    </v-expand-transition>

                    <v-card-text>{{toVoteMessage}}</v-card-text>
                  
                  </v-card>
                </v-hover>
                <div id="WaitMessage">
                  Waiting for message...
                </div>
            </v-col>
            
            </v-row>
</template>

<script>
export default {
    name:'ChatVote',
    props: ["socket", "toVoteMessage", "toVoteUserID"],
    methods:{
      LikeMessage(){
        this.socket.emit("vote response", {userID: this.toVoteUserID, isUpvoted: true})        
        document.getElementById("VoteMessage").hidden = true
        document.getElementById("WaitMessage").hidden = false
      }
    },
    data() {}
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
