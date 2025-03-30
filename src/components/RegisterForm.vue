<template>
  <v-container>
    <v-form v-model="valid" ref="form" @submit.prevent="submitForm">
      <v-text-field
        v-model="form.name"
        :rules="[nameRules.required]"
        label="Name"
        required
      >
      </v-text-field>
      <v-text-field
        v-model="form.email"
        :rules="[emailRules.required, emailRules.format]"
        label="Email"
        required
      >
      </v-text-field>
      <v-text-field
        v-model="form.password"
        :rules="[passwordRules.required]"
        label="Password"
        type="password"
        required
      >
      </v-text-field>
      <v-list dense>
        <v-list-item v-for="(rule, index) in passwordRuleList" :key="index">
          <v-list-item-content>
            <v-row align="center">
              <v-col v-if="rule.isValid" cols="auto">
                <v-icon color="green" small>mdi-check-circle</v-icon>
              </v-col>
              <v-col cols="auto">
                <span :style="rule.isValid ? { color: 'green' } : {}">
                  {{ rule.text }}
                </span>
              </v-col>
            </v-row>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <v-text-field
        v-model="form.confirmPassword"
        :rules="[confirmPasswordRules.required, confirmPasswordRules.match]"
        label="Confirm Password"
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
        Submit
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
        name: "",
        email: "",
        password: "",
        confirmPassword: "",
      },

      nameRules: {
        required: (v) => !!v || "Name required",
      },
      emailRules: {
        required: (v) => !!v || "Valid Email required",
        format: (v) => /.+@.+\..+/.test(v) || "Invalid Email format",
      },
      passwordRules: {
        required: (v) => !!v || "Password required",
      },
      confirmPasswordRules: {
        required: (v) => !!v || "Password confirmation is required",
        match: (v) => v === this.form.password || "Passwords do not match",
      },

      passwordRuleList: [
        { text: "At least 8 characters", isValid: false },
        { text: "At least one uppercase letter", isValid: false },
        { text: "At least one special character", isValid: false },
        { text: "At least one number", isValid: false }, // New rule
      ],
    };
  },
  watch: {
    "form.password": function (newPassword) {
      this.passwordRuleList[0].isValid = newPassword.length >= 8;
      this.passwordRuleList[1].isValid = /[A-Z]/.test(newPassword);
      this.passwordRuleList[2].isValid = /[!@#$%^&*(),.?":{}|<>]/.test(
        newPassword
      );
      this.passwordRuleList[3].isValid = /\d/.test(newPassword);

      this.valid =
        this.passwordRuleList.every((rule) => rule.isValid) &&
        this.form.email &&
        this.form.name &&
        this.form.confirmPassword === this.form.password;
    },
  },
  methods: {
    submitForm() {
      console.log("Form submitted", this.form);
    },
  },
};
</script>

<style scoped>
.v-list-item-content {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.v-list-item-content span {
  margin-left: 8px;
}
.v-divider {
  margin-top: 16px;
}

.v-row {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
</style>
