<template>
  <v-app>
    <auth-page></auth-page>
  </v-app>
</template>

<script>
import AuthPage from "./pages/auth-page/index.vue";

export default {
  name: "App",

  components: {
    "auth-page": AuthPage,
  },

  data: () => ({
    //
  }),
};
</script>

<style scoped></style>
