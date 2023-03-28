<template>
  <v-container fluid pa-0 ma-0 class="wrapper">
    <v-row class="mb-12">
      <v-col xs-12 md-6 lg-6 xl-6 class="form_wrapper">
        <v-sheet>
          <the-form></the-form>
        </v-sheet>
      </v-col>
      <v-col cols="6" class="hidden-sm-and-down">
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

.form_wrapper {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
}
</style>
