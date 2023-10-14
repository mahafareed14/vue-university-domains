<template>
  <v-app-bar
    color="teal-darken-4"
    image="https://picsum.photos/1920/1080?random"
  >
    <template v-slot:image>
      <v-img
        gradient="to top right, rgba(19,84,122,.8), rgba(128,208,199,.8)"
      ></v-img>
    </template>
    <v-app-bar-title>University Domain</v-app-bar-title>
    <v-spacer></v-spacer>
  </v-app-bar>
</template>
<script>
export default {
  name: "AppBar",
};
</script>
