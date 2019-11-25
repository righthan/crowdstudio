<template>
  <v-row>
    <v-col>
      <v-card
        class="pa-2"
        tile
        outlined
        style="height: 220px;"
      >        
        <v-row class="mt-2 mb-2" justify=center align=center>
          <v-col cols="9">
            <v-hover v-slot:default="{ hover }">
              <v-card color="#F3E5F5">
                
                <v-expand-transition>
                  <div
                    v-if="hover"
                    class="d-flex transition-fast-in-fast-out white darken-2 v-card--reveal display-3"
                    style="height: 100%;"
                  >
                    <v-btn text icon color="deep-purple">
                       <v-icon>mdi-thumb-up</v-icon>
                    </v-btn>
                  </div>
                </v-expand-transition>

                <v-card-text>Message Message Message Message Message Message</v-card-text>
                
                </v-card>
            </v-hover>
          </v-col>
          
        </v-row>

        <v-divider :inset="inset"></v-divider>

        {{usrMessage}}
        <v-textarea
          v-model="message"
          append-outer-icon='mdi-send'
          @click:append-outer="sendMessage"
          @keydown="OnKeydown"
          autofocus
          label="'shift+Enter' will send a message."
          outlined
          filled
          rows="3"
        />

      </v-card>
    </v-col>
  </v-row>
  
</template>

<script>
export default {
  name: 'SendMessage',
  data: function () {
    return {
      isTargetViewer: true,
      message: '', 
    }
  },

  computed: {
    usrMessage: function () {
      if (this.isTargetViewer === true) {
        return "> All viewers (Press 'tab' to send to streamer)"
      }
      else {
        return "> Streamer (Press 'tab' to send to all viewers)"
      }
    },
  },

  methods: {
    OnKeydown: function (event) {
      if (event.key === "Tab") {
        event.preventDefault()
        this.isTargetViewer = !this.isTargetViewer
      }
      else if (event.key === "Enter" && event.shiftKey) {
        event.preventDefault()
        this.sendMessage()
      }
    },
    sendMessage: function () {
      this.message = ''
      console.log("TEMP: Send a message")
    }
  }
}
</script>

<style>
.v-card--reveal {
  align-items: center;
  bottom: 0;
  justify-content: center;
  opacity: .8;
  position: absolute;
  width: 100%;
}
</style>
