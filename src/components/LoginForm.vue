<template>
  <div>
    <form @submit.prevent="login">
      <input type="email" v-model="email" placeholder="Email" required />
      <input
        type="password"
        v-model="password"
        placeholder="Password"
        required
      />
      <button type="submit">Log in</button>
    </form>
  </div>
</template>

<script>
import { ref } from "vue";
import { supabase } from "../supabase";

export default {
  name: "LoginForm",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async login() {
      const { error } = await supabase.auth.signIn({
        email: this.email,
        password: this.password,
      });

      if (error) {
        console.error(error);
      } else {
        this.$router.push("/");
      }
    },
  },
};
</script>
