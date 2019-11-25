<template>
    
    <v-row class="mt-2 mb-2" justify=center align=center style="height:100px">

            <v-col cols="9" id="Chatbot">
                <v-hover v-slot:default="{ hover }" id="VoteMessage">
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

                    <v-card-text>Message Message Message Message Message Message</v-card-text>
                    
                    </v-card>
                </v-hover>
            </v-col>
            
            </v-row>
</template>

<script>
export default {
    name:'ChatVote',

    methods:{
    LikeMessage(){

    },
    countDownTimer() {
                if(this.countDown > 0) {
                    setTimeout(() => {
                        this.countDown -= 1
                        this.countDownTimer()
                    }, 1000)
                    }
                if(this.countDown==0) {
                  document.getElementById("VoteMessage").remove()
                }
            }
  },
  data() {
            return {
                countDown : 10
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
