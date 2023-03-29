<template>
  <div class="form">
    <v-img :src="logo" width="48" height="36"></v-img>
    <v-card-title class="form_title">Log in to your account</v-card-title>
    <form>
      <label for="email" class="form_label">Email</label>
      <v-text-field
        class="form_input"
        outlined
        single-line
        height="44"
        dense
        :append-icon="emailErrors.length >= 1 ? 'mdi-alert-circle-outline' : ''"
        v-model="email"
        :error-messages="emailErrors"
        required
        @input="$v.email.$touch()"
        @blur="$v.email.$touch()"
      ></v-text-field>
      <label for="password" class="form_label">Password</label>
      <v-text-field
        class="form_input"
        outlined
        single-line
        height="44"
        dense
        :append-icon="password.length < 8 ? 'mdi-alert-circle-outline' : ''"
        v-model="password"
        :rules="[rules.required, rules.min]"
        :type="show1 ? 'text' : 'password'"
        name="input-10-1"
        hint="At least 8 characters"
        @click:append="show1 = !show1"
      ></v-text-field>
      <div class="form_chache">
        <div class="form_checkbox">
          <v-checkbox
            v-model="checkbox"
            class="form_checkbox"
            :error-messages="checkboxErrors"
            required
            @change="$v.checkbox.$touch()"
            @blur="$v.checkbox.$touch()"
          ></v-checkbox>
          <label class="checkbox_label" for="checkbox">Remember me</label>
        </div>
        <span>Forgot password</span>
      </div>
      <v-btn
        class="mr-4 primary white--text"
        elevation="0"
        height="44"
        @click="submit"
        block
        style="text-transform: none"
        >Sign in
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
      !this.$v.checkbox.checked && errors.push("Agree to continue");
      console.log(errors);
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
    },
  },
  emits: ["submit"],
};
</script>

<style lang="scss">
.form {
  width: 360px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 20px;
  font-family: "Inter";

  @media screen and (max-width: 400px) {
    width: 320px;
  }

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
    height: 28px;
    margin-bottom: 24px;
  }

  &_help {
    text-align: center;
    margin-top: 32px;
    color: #475467;
    font-size: 14px;
    font-weight: 400;
  }

  &_label {
    font-size: 14px;
    font-weight: 500;
    display: block;
    margin-bottom: 6px;
  }

  &_checkbox {
    position: relative;
  }

  &_input {
    font-family: "Inter";
    position: relative;

    & .v-input__slot {
      border-radius: 8px;
    }

    & .v-text-field__details {
      display: block;
      margin-top: 6px;
    }

    & .v-messages__message {
      position: absolute;
      left: -12px;
      bottom: 2px;
    }

    & .mdi-alert-circle-outline::before {
      position: absolute;
      width: 14px;
      height: 14px;
      top: -9px;
      right: -4px;
    }
  }
}

form {
  width: 100%;
  position: relative;
}

span {
  color: #6941c6;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
}

.checkbox_label {
  position: absolute;
  width: 100px;
  bottom: 22px;
  left: 30px;
  font-size: 14px;
  font-weight: 500;
}

.v-text-field--outlined.v-input--has-state fieldset {
  border: 1px solid #f04438;
  display: inline-block;
}

.v-text-field--outlined.v-input--is-focused fieldset {
  border: 1px solid #7f56d9;
  display: block;
}

.v-application .primary--text {
  color: #f9f5ff;
}

.mdi-checkbox-marked::before {
  content: url("../assets/icons/checkbox.svg");
}

.mdi-checkbox-blank-outline::before {
    content: url("../assets/icons/ckeckbox-default.svg");
}

.v-application .error--text {
  .mdi-checkbox-blank-outline::before {
    content: url("../assets/icons/ckeckbox-error.svg");
}
}
</style>
