<template>
  <v-app>
    <Header />
    <v-content>
      <v-container fluid class="grey lighten-5">
        <v-row
          align="stretch"
          text-center
          wrap
        >
          <v-col cols="9">

            <live-stream />
            <v-row>
              <v-col cols="6">
                <rank-message-special/>
              </v-col>
              <v-col cols="6">
                <status/>
              </v-col>
            </v-row>

          </v-col>

          <v-col cols="3">
            <chat-stream/>
            <send-message/>
          </v-col>

        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import Header from '../components/Header.vue'
import Status from '../components/Status.vue'
import LiveStream from '../components/LiveStream.vue'
import SendMessage from '../components/SendMessage.vue'
import ChatStream from '../components/ChatStream.vue'
import RankMessageSpecial from '../components/RankMessageSpecial.vue'

export default {
  name: 'Index',
  components: {
    Header,
    LiveStream,
    SendMessage,
    ChatStream,
    RankMessageSpecial,
    Status,
  },

  data: () => ({
    //
  }),
};
</script>
