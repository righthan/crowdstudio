<template>
  <v-row>
    <v-col>
      <v-card
        class="pa-2"
        tile
        outlined
        style="height: 550px;"
      >
        ChatStream
        <message-normal/>
        <message-special/>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import MessageNormal from './MessageNormal.vue'
import MessageSpecial from './MessageSpecial.vue'

export default {
  name: 'ChatStream',
  components: {
    MessageNormal,
    MessageSpecial,
  }
}
</script>