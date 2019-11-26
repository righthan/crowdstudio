<template>
  <v-card
    class="pa-2"
    tile
    outlined
    style="height: 500px;"
  >
    <iframe src="https://player.twitch.tv/?channel=tvcrank" frameborder="0" allowfullscreen="false" scrolling="no" height="85%" width="100%"></iframe>
    <div id="over"> {{specialMessage}} </div>
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
  name: 'LiveStream',
  data: function () {
    return {
      specialMessage: '',
    }
  }
}
</script>

<style scoped>
.video_info {
  padding-top: 0px;
  padding-bottom: 0px;
}

#over {
  position: absolute;
  color:orange;
  font-size:2em;
  bottom: 20%;
  left: 10%;
  z-index:2;
  background-color: rgba(0,0,0,0.7);
}
</style>
