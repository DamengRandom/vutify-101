<template>
  <nav>
    <v-snackbar v-model="snackbar" :timeout="4000">
      {{ successMessage }}
      <template v-slot:action="{ attrs }">
        <v-btn color="teal" text v-bind="attrs" @click="snackbar = false">
          Close
        </v-btn>
      </template>
    </v-snackbar>
    <v-app-bar app class="text-uppercase dark--text">
      <v-icon
        class="mr-2"
        transition="scale-transition"
        @click="toggleDrawer(!drawer)"
        >{{ changeIcon }}</v-icon
      >
      <v-toolbar-title>
        <span class="font-weight-light pr-1">Trial -</span>
        <span>Vuetify</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn text color="grey">
        <span>Sign Out</span>
        <v-icon right>mdi-lock-outline</v-icon>
      </v-btn>
    </v-app-bar>
    <v-navigation-drawer v-model="drawer" app class="primary">
      <v-layout column align-center>
        <v-flex class="mt-5">
          <v-avatar size="80" class="blue">
            <img src="/" alt="foto" />
          </v-avatar>
          <p class="subheading text-center">title</p>
        </v-flex>
        <v-flex class="mt-4 mb-3">
          <Popup
            @projectAdded="snackbar = true"
            @closeNavbar="drawer = false"
          />
        </v-flex>
      </v-layout>
      <v-list v-for="link in links" :key="link.text">
        <router-link :to="link.route" name="link.text">
          <v-list-item>
            <v-list-item-action class="mr-2">
              <v-list-item-action-text>
                <v-icon>{{ link.icon }}</v-icon>
              </v-list-item-action-text>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title>{{ link.text }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </router-link>
      </v-list>
    </v-navigation-drawer>
  </nav>
</template>

<script>
import Popup from "./Popup";
export default {
  name: "Navbar",
  data() {
    return {
      drawer: false,
      menuIcon: "mdi-menu",
      links: [
        { icon: "mdi-home", text: "Dashboard", route: "/" },
        { icon: "mdi-account", text: "About", route: "/about" },
        { icon: "mdi-checkerboard", text: "Playground", route: "/play" }
      ],
      snackbar: false,
      successMessage: "Data has been sent out successfully 🚀🚀"
    };
  },
  computed: {
    changeIcon() {
      return this.drawer ? "mdi-close" : "mdi-menu";
    }
  },
  methods: {
    toggleDrawer(currentToggle) {
      this.drawer = currentToggle;
    }
  },
  components: {
    Popup
  }
};
</script>
<style scoped></style>
