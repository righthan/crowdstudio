<template>
  <v-card
    class="pa-2 text-center"
    tile
    style="height: 300px;" 
  >
     <span class="panel_header_lg">
       Ranks
     </span>
     <v-divider></v-divider>
      <div class="overflow-y-auto" id="scroll-target" style="max-height: 250px;">
        <v-col class="text-center" >

          <div v-for="(message, index) in rankList" :item="message" :key="index">
              <vote-message-special @clickLike="updateLiked" :message="message.text" :rank="index+1" 
                                    :numLiked="message.numLiked" :numShown="message.numShown"> 
              </vote-message-special>
          </div>

        </v-col>
      </div>
    
  </v-card>
</template>

<script>
import VoteMessageSpecial from '../components/VoteMessageSpecial.vue'

export default {
  name: 'RankMessageSpecial',
  props: ["socket"],
  mounted() {
    this.socket.on("rank list update", (list) => {
      // update rank list
      let urlParams = new URLSearchParams(window.location.search);
      let userID = urlParams.get('userID');
      this.rankList = list.map((msg) => {
          return {text: msg.text, liked: msg.shownUsers.includes(userID), numLiked: msg.likedUsers.length, numShown: msg.shownUsers.length}
      })
    })
  },
  components: {
    VoteMessageSpecial,
  },
  data: function() {
    return {
      specialMsg: "WTF",
      likeStatus: true,
      rankList: [],
    };
  },
  methods: {
    // changes the "liked" status of the messages user has liked
    updateLiked(variable1, variable2) {
      this.specialMsg = this.rankList[variable2-1].text;
      this.rankList[variable2-1].liked = variable1;

      // change the score of the liked message when clicked by the user
      if (variable1 == true){
        this.rankList[variable2-1].score += 1;
        //alert(this.rankList[variable2-1].score);
      }
      else {
        this.rankList[variable2-1].score -= 1;
        //alert(this.rankList[variable2-1].score);
      }
    }
  },
}
</script>