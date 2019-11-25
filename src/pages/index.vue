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

            <live-stream :socket="socket"/>
            <v-row>
              <v-col cols="6">
                <rank-message-special :socket="socket"/>
              </v-col>
              <v-col cols="6">
                <status :socket="socket"/>
              </v-col>
            </v-row>
          {{test}}
          </v-col>

          <v-col cols="3">
            <chat-stream :socket="socket"/>
            <send-message :socket="socket"/>
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

import io from 'socket.io-client';

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
    socket: io('localhost:3001')
  }),
  mounted() {
    let urlParams = new URLSearchParams(window.location.search);
    let userID = urlParams.get('userID');
    this.socket.emit("register", userID);
  },
};
</script>
