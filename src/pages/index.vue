<template>
  <v-container fluid class="grey lighten-5">
    <v-row
      align="stretch"
      text-center
      wrap
    >
      <v-col cols="9">

        <live-stream />
        <v-row>
          <v-col cols="4">
            <rank-message-special/>
          </v-col>
          <v-col cols="4">
            <v-card
              class="pa-2"
              tile
              style="height: 300px;"
            >
              STATUS
            </v-card>
          </v-col>
          <v-col cols="4">
            <v-card
              class="pa-2"
              tile
              style="height: 300px;"
            >
              
            </v-card>
          </v-col>
        </v-row>

      </v-col>

      <v-col cols="3">
        <chat-stream/>
        <send-message/>
      </v-col>

    </v-row>
  </v-container>
</template>

<script>
import LiveStream from '../components/LiveStream.vue'
import SendMessage from '../components/SendMessage.vue'
import ChatStream from '../components/ChatStream.vue'
import RankMessageSpecial from '../components/RankMessageSpecial.vue'

export default {
  name: 'Index',
  components: {
    LiveStream,
    SendMessage,
    ChatStream,
    RankMessageSpecial,
  },

  data: () => ({
    //
  }),
};
</script>
