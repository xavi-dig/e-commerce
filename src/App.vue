<template>
  <div>
    <button @click="logout">Log out</button>
  </div>
</template>

<script>
import { supabase } from "../supabase";

export default {
  name: "LogoutButton",
  methods: {
    async logout() {
      const { error } = await supabase.auth.signOut();

      if (error) {
        console.error(error);
      } else {
        this.$router.push("/");
      }
    },
  },
};
</script>
