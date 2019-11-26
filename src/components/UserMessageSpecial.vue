<template>
    <v-row align="center" justify="center">
        <v-col id="rank" cols="2">
            <div class="text-center title grey--text">{{message.rank}}</div>
            <div class="text-center"><v-icon large justify-center color="purple">{{message.arrow}}</v-icon></div>
        </v-col>

        <v-col id="message" cols="8">
            <v-card color="#F3E5F5"><v-card-text>{{message.content}}</v-card-text></v-card>
        </v-col>

        <v-col cols="2">
            <v-btn id="dbtn"  @click="DeleteMessage()" class="white--text" color="red" icon outlined><v-icon>mdi-delete</v-icon></v-btn>    
        </v-col>
    </v-row>
</template>

<script>
export default {
  name: 'UserMessageSpecial',
  data: () =>({
      message: {content:"Message Message Message Message Message Message", rank:"10", arrow:"mdi-arrow-up"}
  }),
    methods:{
        DeleteMessage(){
            document.getElementById("rank").remove()
            document.getElementById("message").remove()
            document.getElementById("dbtn").remove()
            
        }
    }
}
</script>