<template>
  <div class="login">
    <h1>Login</h1>
    <LoginForm></LoginForm>
  </div>
</template>
<script>
import LoginForm from "@/components/LoginForm.vue";

export default {
  name: "login",
  components: {
    LoginForm,
  },
};
</script>
