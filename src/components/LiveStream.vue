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