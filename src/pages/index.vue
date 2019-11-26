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
          <v-col cols="8">
            <live-stream :socket="socket"/>
            <v-row>
              <v-col cols="6">
                <rank-message-special :socket="socket"/>
              </v-col>
              <v-col cols="6">
                <message-voter :socket="socket"/>
              </v-col>
            </v-row>
          {{test}}
          </v-col>
          <v-col cols="4">
            <chat-stream :socket="socket"/>
            <status :socket="socket"/>
            <send-message :socket="socket"/>
          </v-col>

        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import Header from '../components/Header.vue'
import MessageVoter from '../components/MessageVoter.vue'
import LiveStream from '../components/LiveStream.vue'
import SendMessage from '../components/SendMessage.vue'
import ChatStream from '../components/ChatStream.vue'
import RankMessageSpecial from '../components/RankMessageSpecial.vue'
import Status from '../components/Status.vue'
import "@/assets/global.css"

import io from 'socket.io-client';

export default {
  name: 'Index',
  components: {
    Header,
    LiveStream,
    SendMessage,
    ChatStream,
    RankMessageSpecial,
    MessageVoter,
    Status,
  },
  data: () => ({
    socket: io('https://ec2-54-180-96-9.ap-northeast-2.compute.amazonaws.com:3000')
  }),
  mounted() {
    let urlParams = new URLSearchParams(window.location.search);
    let userID = urlParams.get('userID');
    this.socket.emit("register", userID);
  },
};
</script>
