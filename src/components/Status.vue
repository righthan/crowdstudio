<template>
    <v-card
    class="pa-2 text-center title"
    tile
    style="height: 300px;"
    >
        Your Current Message
    <v-divider :inset="inset"></v-divider>
        <v-container>
            <v-layout row justify-space-around mt-12 mb-12 align-center>
                <v-flex md2 l2 xl2>
                    <div class="text-center title grey--text">{{message.rank}}</div>
                    <div class="text-center"><v-icon large justify-center color="purple">{{message.arrow}}</v-icon></div>

                </v-flex>
                <v-flex md9 l9 xl9>
                    <v-card color="#F3E5F5"><v-card-text>{{message.content}}</v-card-text></v-card>

                </v-flex>
            </v-layout>
            <v-layout row justify-center align-center>
                <v-flex xs5 s5 md-auto>
                    <v-btn class="white--text" color="red">Delete<v-icon right>mdi-delete</v-icon></v-btn>
                </v-flex>
            </v-layout>
        </v-container>
    
    </v-card>

</template>

<script>
export default {
  name: 'Status',
  data: () =>({
      message: {content:"Message Message Message Message Message Message", rank:"10", arrow:"mdi-arrow-up"}
  })

}
</script>
