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
          {{view_count}} viewers
        </span>
      </v-col>
    </v-row>
  </v-card>
</template>

<script>
export default {
  name: 'LiveStream',
  props: ["socket"],
  data: () => ({
    view_count: 0
  }),
  mounted() {
    this.socket.on("view count update", count => {
      this.view_count = count
    })
  }
}
</script>

<style scoped>
.video_info {
  padding-top: 0px;
  padding-bottom: 0px;
}
</style>
