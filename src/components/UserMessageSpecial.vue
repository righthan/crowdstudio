<template>
    <v-row align="center" justify="center">
        <v-col cols="10" v-if="!message && !messageDied" style="color: gray">
          You have no message to the streamer.
        </v-col>
        <v-col cols="10" v-if="!message && messageDied" style="color: red">
          Your message was not popular enough...
        </v-col>
        <v-col id="rank" cols="2" v-if="message">
            <div class="text-center title grey--text">{{message ? message.rank : ""}}</div>
            <div class="text-center"><v-icon large justify-center color="purple">{{message ? message.arrow : ""}}</v-icon></div>
        </v-col>
        <v-col id="message" cols="8" v-if="message">
            <v-card color="#F3E5F5"><v-card-text>{{message ? message.content : ""}}</v-card-text></v-card>
        </v-col>

        <v-col cols="2" v-if="message">
            <v-btn id="dbtn"  @click="DeleteMessage()" class="white--text" color="red" icon outlined><v-icon>mdi-delete</v-icon></v-btn>    
        </v-col>
    </v-row>
</template>

<script>
export default {
  props: ['socket'],
  name: 'UserMessageSpecial',
  data: () =>({
      message: null,
      messageDied: false
  }),
  mounted() {
    this.socket.on("msg status update", (msg) => {
      if(msg == null){
        // if no current message
        this.HideMessage()
      }else{
        // check if new rank is less or more than old rank
        this.ShowMessage()
        var arrow = "mdi-minus"
        if(this.message && msg.rank > this.message.rank)
            arrow = "mdi-arrow-up"
        else if(this.message && msg.rank < this.message.rank)
            arrow = "mdi-arrow-down"
        this.message = {content: msg.content, rank: msg.rank, arrow: arrow}
      }
    })

    this.socket.on("message died", () => {
      this.messageDied = true
      setTimeout(() => {
        this.messageDied = false
      }, 10000)
    })
  },
    methods:{
        DeleteMessage(){
            this.HideMessage()
            this.socket.emit("delete special")
        },
        HideMessage(){
            document.getElementById("rank").hidden = true
            document.getElementById("message").hidden = true
            document.getElementById("dbtn").hidden = true
        },
        ShowMessage(){
            document.getElementById("rank").hidden = false
            document.getElementById("message").hidden = false
            document.getElementById("dbtn").hidden = false
        }
    }
}
</script>