<template>

  <v-row>
    <v-col cols="3">
      <div style="color: green; font-weight: bold;">
        {{user}}
      </div>
    </v-col>
    <v-col cols="9">
      <div style="color: purple; font-weight: bold;">
        {{message}}
      </div>
    </v-col>
  </v-row>

  
</template>

<script>
export default {
  name: 'MessageSpecial',
  data: () => ({

  }),
  props: {
    message: String,
    user: String,
  }
}
</script>