<template>
  <v-card
    class="pa-2 text-center title"
    tile
    style="height: 300px;"
    
  >
    Ranks
     <v-divider></v-divider>
      <div class="overflow-y-auto" id="scroll-target" style="max-height: 250px;">
        <v-col class="text-center" >

          <div v-for="(message, index) in rankList" :item="message" :key="index">
              <vote-message-special @clickLike="updateLiked" :message="message.text" :rank="message.rank"> </vote-message-special>
          </div>

        </v-col>
      </div>
    
  </v-card>
</template>

<script>
import VoteMessageSpecial from '../components/VoteMessageSpecial.vue'

export default {
  name: 'RankMessageSpecial',
  components: {
    VoteMessageSpecial,
  },
  data: function() {
    return {
      specialMsg: "WTF",
      likeStatus: true,
      rankList: [
        {text: 'first message', liked: false, rank: 1},
        {text: 'second message', liked: false, rank: 2},
        {text: 'third message', liked: false, rank: 3},
        {text: 'fourth message', liked: false, rank: 4},
        {text: 'fifth message', liked: false, rank: 5},
      ],
    };
  },
  methods: {
    // changes the "liked" status of the messages user has liked
    updateLiked(variable1, variable2) {
      this.specialMsg = this.rankList[variable2-1].text;
      this.likeStatus = variable1;
    }
  },
}
</script>