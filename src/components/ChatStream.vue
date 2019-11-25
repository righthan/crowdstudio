<template>
  <v-row>
    <v-col>
      <v-card
        class="pa-2"
        tile
        outlined
        style="height: 550px;"
      >
        <div class="overflow-y-auto" id="scroll-target" style="max-height: 550px;">
          <div v-for="(instance, index) in messageList" :item="instance" :key="index">
            
            <div v-if="instance.msgState == true">
              <message-special :message="instance.message" :user="instance.UserName"/>
            </div>

            <div v-else>
              <message-normal :message="instance.message" :user="instance.UserName"/>
            </div>

          </div>
        </div>

      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import MessageNormal from './MessageNormal.vue'
import MessageSpecial from './MessageSpecial.vue'

export default {
  name: 'ChatStream',
  props: ["socket"],
  components: {
    MessageNormal,
    MessageSpecial,
  },
  mount() {
    this.socket.on("message", (msg) => {
      msg
      // display message
    })
  },
  data: function() {
    return {
      
      
      // for msgState
      //true == Special, false == normal
      
      messageList: [
        {message: "sample message blah blah blah", msgState: true, UserName: "User 1"},
        {message: "sample message blah blah blah", msgState: false, UserName: "User 2"},
        {message: "sample message blah blah blah", msgState: false, UserName: "User 2"},
        {message: "sample message blah blah blah", msgState: false, UserName: "User 2"},
        {message: "sample message blah blah blah", msgState: false, UserName: "User 2"},
        {message: "sample message blah blah blah", msgState: true, UserName: "User WTF"},
        {message: "sample message blah blah blah", msgState: false, UserName: "User 2"},
        {message: "sample message blah blah blah", msgState: false, UserName: "User 2"},
        {message: "sample message ", msgState: false, UserName: "User 2"},
      ]
    }
  }
}
</script>