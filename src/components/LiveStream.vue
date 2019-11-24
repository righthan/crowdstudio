<<<<<<< HEAD
<template>
  <v-card
    class="pa-2"
    tile
    outlined
    style="height: 500px;"
  >
    LiveStream
    <help/>
  </v-card>
</template>

<script>
import Help from './Help.vue'

export default {
  name: 'LiveStream',
  components: {
    Help,
  }
}
</script>
=======
<template>
  <v-card
    class="pa-2"
    tile
    outlined
    style="height: 500px;"
  >
    <iframe src="https://player.twitch.tv/?channel=tvcrank" frameborder="0" allowfullscreen="true" scrolling="no" height="85%" width="100%"></iframe>
    <v-divider/>
    <v-row>
      <v-col cols="6" align-self="start" class = "video_info">
        <h2>
          We are the crowdstudio!
        </h2>
        <a href="https://youtube.com">Yollllo</a>
      </v-col>
      <v-col cols="6">
        <span style="float: right;">
          <v-icon>
            mdi-account
          </v-icon>
          1,000 viewers
        </span>
      </v-col>
    </v-row>
  </v-card>
</template>

<script>
export default {
  name: 'LiveStream'
}
</script>

<style scoped>
.video_info {
  padding-top: 0px;
  padding-bottom: 0px;
}
</style>
>>>>>>> 4c6876f194fc4048149fd97685437a55e392899b
