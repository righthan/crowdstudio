<template>

    <v-col cols="6" id="VoteMessage2" v-if="liked == true && toVoteID">
            <v-hover v-slot:default="{ hover }"  >
                <v-card flat id="message2" color="#F3E5F5" disabled>
                    

                <v-card-text>{{toVoteMsg}}}</v-card-text>
                
                </v-card>
            </v-hover>
        </v-col>
    
    
     <v-col cols="6" id="VoteMessage2" v-else-if="toVoteID">
            <v-hover v-slot:default="{ hover }" >
                <v-card id="message2" color="gray">
                    
                <v-expand-transition>
                <div
                    id = "firstHover"
                    v-on:click ="like"
                    v-if="hover"
                    class="d-flex transition-fast-in-fast-out white darken-2 v-card--reveal display-3"
                    style="height: 100%; cursor:pointer;"
                >
                    <v-icon color="deep-purple">mdi-thumb-up</v-icon>
                </div>
                </v-expand-transition>

                <v-card-text>{{toVoteMsg}}</v-card-text>
                
                </v-card>
            </v-hover>
        </v-col>

</template>

<script>
export default{
    name : 'Candidate2',
    props: ["socket", "toVoteID", "toVoteMsg"],
    data(){
        return{
            liked: false,
        }
    },
    methods: {
      like: function() {
          this.liked = !this.liked;
          this.socket.emit("vote response", {userID: this.toVoteID, isUpvoted: true})
      },
 
  },
  

}
</script>