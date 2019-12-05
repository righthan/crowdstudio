<template>
  <v-card
    class="pa-2"
    tile
    outlined
    style="height: 500px;"
  >
    <iframe width="100%" height="85%" src="https://www.youtube.com/embed/7oQ7G7GvfHs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    <div id="over"> {{specialMessage}} </div>
    <v-divider/>
    <v-row>
      <v-col cols="10" align-self="start" class = "video_info">
        <h2>
          [카이스트 원탑 효준이가 보여주는 롤토체스] 마! 이게 롤토체스다!!!
        </h2>
        카이스트원탑효준
      </v-col>
      <v-col cols="2">
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

var voice = ''

// list of languages is probably not loaded, wait for it
if(window.speechSynthesis.getVoices().length == 0) {
  window.speechSynthesis.addEventListener('voiceschanged', function() {
    speechSetup();
  });
}
else {
  // languages list available, no need to wait
  speechSetup()
}

function speechSetup() {
  // get all voices that browser offers
  var available_voices = window.speechSynthesis.getVoices();

  // find voice by language locale "en-US"
  // if not then select the first voice
  for(var i=0; i<available_voices.length; i++) {
    if(available_voices[i].lang === 'ko-KR') {
      voice = available_voices[i];
      break;
    }
  }
  if(voice === '')
    voice = available_voices[0];
}

function textToSpeech(text){
  // new SpeechSynthesisUtterance object
  var utter = new SpeechSynthesisUtterance();
  utter.rate = 0.8;
  utter.pitch = 0.5;
  utter.text = text;
  utter.voice = voice;

  // speak
  window.speechSynthesis.speak(utter);
}

export default {
  name: 'LiveStream',
  props: ["socket", "userID"],
  mounted() {
    this.socket.on("view count update", count => {
      this.view_count = count
    })

    this.socket.on("sound message", (msg) => {

      if(this.userID === "streamer"){
        textToSpeech(msg.text)
        this.specialMessage = msg.text
        setTimeout(() => {
          this.specialMessage = ""
        }, 10000)
      }else{
        setTimeout(() => {
          this.specialMessage = msg.text
          setTimeout(() => {
            this.specialMessage = ""
          }, 10000)
        }, 10000)
      }
    })
  },
  data: function () {
    return {
      specialMessage: '',
      view_count: 0
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
