<template>
    <div v-if="liked == true">
        <v-row align="center" justify="center">
            <v-col cols="1">
                <h2 class="purple--text"> {{rank}} </h2>
            </v-col>

            <v-col cols="10">

            <v-hover v-slot:default="{ hover }">
                <v-card  disabled flat color="#F3E5F5">
                    <v-card-text>{{message}}</v-card-text>
                </v-card>
            </v-hover>
            
            </v-col>
            <v-col cols="1">
                {{numLiked}}/{{numShown}}
            </v-col>

        </v-row>
    </div>
    <div v-else>
        <v-row justify="center" align="center">
            <v-col cols="1">
                <h2 class="purple--text"> {{rank}} </h2>
            </v-col>

            <v-col cols="10">

                <v-hover v-slot:default="{ hover }">
                <v-card color="gray">
                    <v-card-text>{{message}}</v-card-text>
                </v-card>
            </v-hover>
            
            </v-col>
            <v-col cols="1">
                {{numLiked}}/{{numShown}}
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
    numLiked: Number,
    numShown: Number
  },
  methods: {
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