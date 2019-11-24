<template>
    <v-card
        class="pa-2"
        tile
        style="height: 300px;"
    >
        Message Status
    <v-divider :inset="inset"></v-divider>
        <v-container>
            <v-row class="mt-8 mb-8 ml-1">
                <v-col cols="2">
                    <div class="text-center title grey--text">{{message.rank}}</div>
                    <div class="text-center"><v-icon large justify-center color="purple">{{message.arrow}}</v-icon></div>

                </v-col>
                <v-col cols="9">
                    <v-card color="#F3E5F5"><v-card-text>{{message.content}}</v-card-text></v-card>

                </v-col>
            </v-row>
            <v-row justify="center">
                    <v-btn class="white--text" color="red">Delete<v-icon right>mdi-delete</v-icon></v-btn>
            </v-row>
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
