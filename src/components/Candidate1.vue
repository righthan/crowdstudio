<template>
    
     <v-col cols="8" v-if="toVoteID" id="VoteMessage1">
            <v-hover v-slot:default="{ hover }" >
                <v-card id="message1" :color="liked ? '#F3E5F5' : 'gray'" height="100%">
                    
                <v-expand-transition>
                <div
                    id = "firstHover"
                    v-on:click ="like"
                    v-if="hover"
                    class="d-flex transition-fast-in-fast-out white darken-2 v-card--reveal display-3"
                    style="height: 100%; cursor:pointer;"
                >
                    <v-icon color="deep-purple">{{liked ? "mdi-thumb-down" : "mdi-thumb-up"}}</v-icon>
                </div>
                </v-expand-transition>

                <v-card-text>{{toVoteMsg}}</v-card-text>
                
                </v-card>
            </v-hover>
        </v-col>


</template>

<script>
export default{
    name : 'Candidate1',
    props: ["socket", "toVoteID", "toVoteMsg", "liked"],
    methods: {
      like: function() {
          this.$emit('likeSwitch')
      },
      
 
  },
  

}
</script>