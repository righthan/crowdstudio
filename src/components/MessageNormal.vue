<template>

  <v-row>
    <v-col cols="3">
      <div style="color: green; font-weight: bold;">
        {{user}}
      </div>
    </v-col>
    <v-col cols="8">
      <div style="color: black">
        {{message}}
      </div>
    </v-col>
  </v-row>

  
</template>

<script>
export default {
  name: 'MessageNormal',
  data: () => ({

  }),
  props: {
    message: String,
    user: String,
  }
}
</script>