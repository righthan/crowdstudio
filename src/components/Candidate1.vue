<template>

    <v-col cols="6"  v-if="liked == true" id="VoteMessage1">
            <v-hover v-slot:default="{ hover }"  >
                <v-card flat id="message1" color="#F3E5F5" disabled>
                    

                <v-card-text>{{messages.message1}}</v-card-text>
                
                </v-card>
            </v-hover>
        </v-col>
    
    
     <v-col cols="6" v-else id="VoteMessage1">
            <v-hover v-slot:default="{ hover }" >
                <v-card id="message1" color="gray">
                    
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

                <v-card-text>{{messages.message1}}</v-card-text>
                
                </v-card>
            </v-hover>
        </v-col>

</template>

<script>
export default{
    name : 'Candidate1',

    data(){
        return{
            countDown : 10,
            messages: {message1:" Message  Message  Message  Message", message2:" Message  Message  Message  Message"},
            liked: false,
            likecounter: 0
        }
    },
    methods: {
      like: function() {
          this.liked = !this.liked;
          this.$emit("clickLike", this.liked, this.rank);
          this.$emit("messageLike");
          this.likecounter += 1;

          if(this.likecounter==2){
              this.countDown=0;
          }
      },
      
 
  },
  

}
</script>