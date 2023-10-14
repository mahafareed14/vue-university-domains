<template>
  <v-app>
    <AppBar />
    <v-main>
      <DropDown />
    </v-main>
  </v-app>
</template>

<script>
import DropDown from "./components/DropDown.vue";
import AppBar from "./components/AppBar.vue";
export default {
  name: "App",

  components: {
    DropDown,
    AppBar,
  },
};
</script>
