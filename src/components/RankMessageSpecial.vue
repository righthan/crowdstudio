<template id="SpecialMessageRanks">
  <v-card
    class="pa-2 text-center title"
    tile
    style="height: 300px;"
  >
    Ranks
     <v-divider :inset="inset"></v-divider>
    
      <v-col class="text-center">
        <div class="my-2 px-0">
          <v-row align="center">
            <div class="my-2 pr-2">
              <h1 class="purple--text"> 1 </h1>
            </div>
            <div class="my-2 px-0 pr-1" style="width: 400px;">
      
                <v-card color="#F3E5F5" style="width: 400px;">
                  <v-card-text>{{rankList[0].text}}</v-card-text>
                </v-card>
              
            </div>
            <v-btn text icon color="deep-purple">
              <v-icon>mdi-thumb-up</v-icon>
            </v-btn>
          </v-row>
        </div>

        <div class="my-2">
          <v-row align="center">
            <div class="my-2 pr-3">
              <h2 class="purple--text"> 2 </h2>
            </div>
            <div class="my-2 px-0 pr-1" style="width: 400px;">
              
                <v-card color="#F3E5F5" style="width: 400px;">
                  <v-card-text>What</v-card-text>
                </v-card>
              
            </div>
            <v-btn text icon color="deep-purple">
              <v-icon>mdi-thumb-up</v-icon>
            </v-btn>
          </v-row>
        </div>
        
        <div class="my-2">
          <v-row align="center">
            <div class="my-2 pr-4">
              <h3 class="purple--text"> 3 </h3>
            </div>
            <div class="my-2 px-0 pr-1" style="width: 400px;">
              
                <v-card color="#F3E5F5" style="width: 400px;">
                  <v-card-text>What</v-card-text>
                </v-card>
              
            </div>
            <v-btn text icon color="deep-purple">
              <v-icon>mdi-thumb-up</v-icon>
            </v-btn>
          </v-row>
        </div>
      </v-col>
    
  </v-card>
</template>

<script>
export default {
  name: 'RankMessageSpecial',
  data: () => ({
    rankList: [
      {text: 'header1', rank: '1', likeBool: 'False'},
      {text: 'header2', rank: '2', likeBool: 'False'}
    ]
  }),
}
</script>