<template>
  <v-card
    class="pa-2"
    tile
    outlined
    style="height: 550px;"
  >
    <div class="overflow-y-auto" id="scroll-target-1" style="max-height: 530px; padding-right : 15px">
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
  mounted() {
    this.socket.on("message", (msg) => {
      this.messageList.push({message: msg.text, msgState: msg.isSpecial, UserName: msg.userID})
      updateScroll()
      // display message
    })
  },
  data: function() {
    return {
      // for msgState
      //true == Special, false == normal
      messageList: [
      ]
    }
  }
}

function updateScroll(){
  var element = document.getElementById("scroll-target-1");
  element.scrollTop = element.scrollHeight;
}

</script>