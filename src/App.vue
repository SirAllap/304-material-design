<template>
  <v-app>
    <NavBar />
    <v-main>
      <LoginForm />
    </v-main>
    <v-footer padless app dark>
      <v-col class="blue-grey darken-3 accent-2 text-center" cols="12">
        {{ new Date().getFullYear() }} — <strong>Reboot</strong>
      </v-col>
    </v-footer>
  </v-app>
</template>

<script>
import LoginForm from "@/components/LoginForm.vue";
import NavBar from "@/components/NavBar.vue";

export default {
  name: "App",

  components: {
    LoginForm,
    NavBar,
  },

  data: () => ({}),
};
</script>

<style scoped></style>
