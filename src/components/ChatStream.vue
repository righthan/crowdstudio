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
    components: {
      MessageNormal,
      MessageSpecial,
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
          {message: "sample message ", msgState: false, UserName: "User 2"},
          {message: "sample message ", msgState: false, UserName: "User 2"},
          {message: "sample message ", msgState: false, UserName: "User 2"},
          {message: "sample message ", msgState: false, UserName: "User 2"},

        ]
      }
    }
  }

  function updateScroll(){
    var element = document.getElementById("scroll-target-1");
    element.scrollTop = element.scrollHeight;
  }

  setInterval(updateScroll,10000);
</script>