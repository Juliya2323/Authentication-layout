<template>
  <v-container fluid pa-0 ma-0 class="wrapper">
    <v-row class="mb-12">
      <v-col cols="6">
        <v-sheet>
          <v-row class="mb-12" justify="center">
            <v-col cols="6">
              <the-form></the-form>
            </v-col>
          </v-row>
        </v-sheet>
      </v-col>
      <v-col cols="6">
        <v-sheet>
          <v-img cover :src="bgImage" class="background"></v-img>
        </v-sheet>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import TheForm from "/src/components/TheForm.vue";
import bgImage from "../../assets/images/bg.png";
export default {
  name: "AuthPage",
  components: {
    TheForm,
  },
  data() {
    return {
      bgImage,
    };
  },
};
</script>

<style scoped>
.wrapper {
  height: 100vh;
}
.background {
  height: 100vh;
}
</style>
