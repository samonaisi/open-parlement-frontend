<template>
  <v-container>
    azeaze
    <v-app-bar :elevation="2">
      <template v-slot:prepend> </template>

      <v-app-bar-title>Open Parlement</v-app-bar-title>
      <v-btn variant="outlined" text to="/login"> Login </v-btn>
      <v-btn text to="/register"> Register </v-btn>
    </v-app-bar>
  </v-container>
</template>

<script>
export default {
  name: "AppBar",
  data: () => ({}),
};
</script>
