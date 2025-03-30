<template>
  <v-container>
    <v-form v-model="valid" ref="form" @submit.prevent="submitForm">
      <v-text-field
        v-model="form.email"
        :rules="[emailRules.required, emailRules.format]"
        label="Email"
        required
      >
      </v-text-field>

      <v-text-field
        v-model="form.password"
        :rules="[passwordRules.required, passwordRules.min]"
        label="Password"
        type="password"
        required
      >
      </v-text-field>

      <v-btn
        :disabled="!valid"
        type="submit"
        color="primary"
        variant="outlined"
      >
        Log In
      </v-btn>
    </v-form>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      valid: false,
      form: {
        email: "",
        password: "",
      },

      emailRules: {
        required: (v) => !!v || "Email is required",
        format: (v) => /.+@.+\..+/.test(v) || "Invalid email format",
      },
      passwordRules: {
        required: (v) => !!v || "Password is required",
        min: (v) =>
          (v && v.length >= 6) || "Password must be at least 6 characters",
      },
    };
  },
  methods: {
    submitForm() {
      console.log("Login form submitted", this.form);
    },
  },
};
</script>

<style scoped>
/* Add custom styles if necessary */
</style>
