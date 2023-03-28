<template>
  <div class="form">
    <v-img :src="logo" width="48px" height="36px"></v-img>
    <v-card-title class="form_title">Log in to your account</v-card-title>
    <form>
      <label for="email">Email</label>
      <v-text-field 
        outlined
        single-line
        class="form_input"
        v-model="email"
        :error-messages="emailErrors"
        label="E-mail"
        required
        @input="$v.email.$touch()"
        @blur="$v.email.$touch()"
      ></v-text-field>
      <label for="password">Password</label>
      <v-text-field 
        outlined
        single-line
        v-model="password"
        :rules="[rules.required, rules.min]"
        :type="show1 ? 'text' : 'password'"
        name="input-10-1"
        label="Password"
        hint="At least 8 characters"
        @click:append="show1 = !show1"
      ></v-text-field>
      <div class="form_chache">
        <v-checkbox
          v-model="checkbox"
          :error-messages="checkboxErrors"
          label="Remember me"
          required
          @change="$v.checkbox.$touch()"
          @blur="$v.checkbox.$touch()"
        ></v-checkbox>
        <span>Forgot password</span>
      </div>
      <v-btn
        class="mr-4 primary white--text"
        elevation="0"
        @click="submit"
        block
      >
        Submit
      </v-btn>
      <p class="form_help">
        Can’t log in to your account? <span>Ask support</span>
      </p>
    </form>
  </div>
</template>

<script>
import logo from "../assets/icons/logo.svg";
import { validationMixin } from "vuelidate";
import { required, email } from "vuelidate/lib/validators";

export default {
  mixins: [validationMixin],

  validations: {
    email: { required, email },
    checkbox: {
      checked(val) {
        return val;
      },
    },
  },

  data: () => ({
    email: "",
    checkbox: false,
    password: "Password",
    show1: false,
    show2: true,
    show3: false,
    show4: false,
    rules: {
      required: (value) => !!value || "Please fill in your password",
      min: (v) => v.length >= 8 || "Min 8 characters",
      emailMatch: () => `The email and password you entered don't match`,
    },
    logo: logo,
  }),

  computed: {
    checkboxErrors() {
      const errors = [];
      if (!this.$v.checkbox.$dirty) return errors;
      !this.$v.checkbox.checked && errors.push("You must agree to continue!");
      return errors;
    },
    emailErrors() {
      const errors = [];
      if (!this.$v.email.$dirty) return errors;
      !this.$v.email.email && errors.push("Must be valid e-mail");
      !this.$v.email.required && errors.push("Please check email address");
      return errors;
    },
  },

  methods: {
    submit() {
      this.$v.$touch();
      console.log(this.$v);
      if (this.$v.$invalid) {
        console.log("invalid");
        return;
      }
      this.$emit("submit", this.formData);
      console.log("submitted!");
    }
  },
  emits: ["submit"],
};
</script>

<style scoped lang="scss">
.form {
  width: 360px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 24px;

  &_title {
    padding: 0;
    font-size: 30px;
    font-weight: 600;
    color: #101828;
    margin-bottom: 6px;
  }

  &_chache {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  &_help {
    text-align: center;
    margin-top: 32px;
    color: #475467;
    font-size: 14px;
    font-weight: 400;
  }
}

form {
  width: 100%;
}

span {
  color: #6941c6;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
}

body .v-application .error--text {
  color: #475467 !important;
  caret-color: #475467 !important;
}


</style>
