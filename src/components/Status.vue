<template>
  <v-row>
    <v-col>
      <v-card
        
        tile
        outlined
        style="height: 120px;"
      >
        <span class="panel_header_sm">Your message to the streamer is now</span>
        <v-divider :inset="inset"/>
        <UserMessageSpecial :socket="socket"/>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import UserMessageSpecial from '../components/UserMessageSpecial.vue'
export default {
  name: 'Status',
  props: ["socket"],
  components:{
      UserMessageSpecial
    },
  data: () =>({
      message: {content:"Message Message Message Message Message Message", rank:10, arrow:"mdi-arrow-up"}
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

<style scoped>
.v-card--reveal {
  align-items: center;
  bottom: 0;
  justify-content: center;
  opacity: .8;
  position: absolute;
  width: 100%;
}

</style>