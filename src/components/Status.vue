<template>
    <v-card
    class="pa-2 text-center title"
    tile
    style="height: 300px;"
    >
        Message Status
        <v-divider :inset="inset"></v-divider>
        <UserMessageSpecial/>
    </v-card>

</template>

<script>
import UserMessageSpecial from '../components/UserMessageSpecial.vue'
export default {
  name: 'Status',
  components:{
      UserMessageSpecial
    },
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
