<template>

    <v-container>
        <v-row class="mt-8 mb-8 ml-1">
            <v-col id="rank" cols="2">
                <div class="text-center title grey--text">{{message ? message.rank : ""}}</div>
                <div class="text-center"><v-icon large justify-center color="purple">{{message ? message.arrow : ""}}</v-icon></div>

            </v-col>
            <v-col id="message" cols="9">
                <v-card color="#F3E5F5"><v-card-text>{{message ? message.content : ""}}</v-card-text></v-card>

            </v-col>
        </v-row>
        <v-row justify="center">
                <v-btn id="dbtn"  @click="DeleteMessage()" class="white--text" color="red">Delete<v-icon right>mdi-delete</v-icon></v-btn>
        </v-row>
    </v-container>



</template>

<script>
export default {
  name: 'Status',
  props: ['socket'],
  data: () =>({
      message: null
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