<template>
  <v-app>
    <v-container fluid pa-0>
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
            <v-img cover :src="bgImage"></v-img>
          </v-sheet>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
import TheForm from '/src/components/TheForm.vue'
import bgImage from "../../assets/images/bg.png"
export default {
  name: "AuthPage",
  components: {
    TheForm
  },
  data() {
    return {
      bgImage
    }
  }
};
</script>

<style scoped></style>
