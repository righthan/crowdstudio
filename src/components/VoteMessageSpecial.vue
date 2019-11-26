<template>
    <div v-if="liked == true">
        <v-row align="center" justify="center">
            <v-col cols="1">
                <h2 class="purple--text"> {{rank}} </h2>
            </v-col>

            <v-col cols="11">

            <v-hover v-slot:default="{ hover }">
                <v-card  disabled flat color="#F3E5F5">
                    <v-card-text>{{message}}</v-card-text>
                </v-card>
            </v-hover>
            
            </v-col>

        </v-row>
    </div>
    <div v-else>
        <v-row justify="center" align="center">
            <v-col cols="1">
                <h2 class="purple--text"> {{rank}} </h2>
            </v-col>

            <v-col cols="11">

                <v-hover v-slot:default="{ hover }">
                <v-card color="gray">
                    <v-expand-transition>
                        <div
                            v-on:click = "like"
                            v-if="hover"
                            class="d-flex transition-fast-in-fast-out white darken-2 v-card--reveal display-3"
                            style="height: 100%; cursor:pointer;"
                        >
                            <v-icon color="deep-purple">mdi-thumb-up</v-icon>
                        </div>
                    </v-expand-transition>
                    <v-card-text>{{message}}</v-card-text>
                </v-card>
            </v-hover>
            
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

<style scoped>
    .v-card--reveal {
    align-items: center;
    bottom: 0;
    justify-content: center;
    opacity: .8;
    position: absolute;
    width: 100%;
    }
</style>