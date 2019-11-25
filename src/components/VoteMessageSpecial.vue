
<template>
    <div v-if="liked == true">
        <v-row align="center">
            <v-col cols="1">
                <h2 class="purple--text"> {{rank}} </h2>
            </v-col>

            <v-col cols="10">

                <v-card color="#F3E5F5">
                    <v-card-text>{{message}}</v-card-text>
                </v-card>
            
            </v-col>

            <v-col cols ="1">
                <v-btn v-on:click="like" text icon color="deep-purple">
                    <v-icon>mdi-thumb-up</v-icon>
                </v-btn>
            </v-col>
        </v-row>
    </div>
    <div v-else>
        <v-row align="center">
            <v-col cols="1">
                <h2 class="purple--text"> {{rank}} </h2>
            </v-col>

            <v-col cols="10">

                <v-card color="gray">
                    <v-card-text>{{message}}</v-card-text>
                </v-card>
            
            </v-col>

            <v-col cols ="1">
                <v-btn v-on:click="like" text icon color="gray">
                    <v-icon>mdi-thumb-up</v-icon>
                </v-btn>
            </v-col>
        </v-row>
    </div>
</template>


<script>
export default {
  name: 'VoteMessageSpecial',
  data() {
    return {
        liked: false,
    };
  },
  props: {
    message: String,
    msgList: Array,
    rank: Number,
  },
  methods: {
      like: function() {
          this.liked = !this.liked;
          this.$emit("clickLike", this.liked, this.rank);
      }
  }
}
</script>