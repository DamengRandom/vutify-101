<template>
  <div>
    <p class="indigo white--text">
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Veritatis
      blanditiis sequi fuga eveniet vero! Temporibus quod rerum, vitae porro,
      quas delectus, consequuntur hic cupiditate sint corporis in expedita
      quidem soluta.
    </p>
    <p class="blue white--text text--darken-8">
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Veritatis
      blanditiis sequi fuga eveniet vero! Temporibus quod rerum, vitae porro,
      quas delectus, consequuntur hic cupiditate sint corporis in expedita
      quidem soluta.
    </p>
    <v-divider class="mt-4"></v-divider>
    <!-- Typography -->
    <h1 class="display-4">Massive display</h1>
    <h5 class="display-1">Smaller display</h5>
    <p class="headline">Headline text</p>
    <p class="subheading">This is a subheading</p>
    <p class="caption">This is a caption</p>
    <v-divider class="mt-4"></v-divider>
    <!-- buttons -->
    <v-btn color="teal white--text" class="mr-2" depressed>click me</v-btn>
    <v-btn text color="teal" class="mr-2" large>click</v-btn>
    <v-btn depressed color="blue" class="mr-2 white--text" small>
      <v-icon left color="white">mdi-email</v-icon>
      <span>Email Me</span>
    </v-btn>
    <v-divider class="mt-4"></v-divider>

    <v-btn fab color="red" small>
      <v-icon color="white">mdi-heart</v-icon>
    </v-btn>

    <v-btn class="hidden-md-and-down">hide when md or sm screen</v-btn>
    <v-btn class="hidden-md-and-up">hide when lg screen</v-btn>
    <v-btn class="hidden-sm-only">hide when only sm screen</v-btn>
    <v-divider class="mt-4"></v-divider>
    <!-- Expansion panels -->
    <div>
      <v-expansion-panels>
        <v-expansion-panel v-for="(item, i) in 5" :key="i">
          <v-expansion-panel-header>
            Item {{ i + 1 }}
          </v-expansion-panel-header>
          <v-expansion-panel-content>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
            eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim
            ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut
            aliquip ex ea commodo consequat.
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
    </div>
    <v-divider class="mt-4"></v-divider>
    <!-- dropdown menu -->
    <v-menu offset-y v-if="items && items[0].title">
      <template v-slot:activator="{ on, attrs }">
        <v-btn color="dark" dark v-bind="attrs" v-on="on">
          Dropdown
        </v-btn>
      </template>
      <v-list>
        <v-list-item v-for="(item, index) in items" :key="index">
          <v-list-item-title>{{ item.title }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
  </div>
</template>
<script>
export default {
  name: "Playground",
  data() {
    return {
      items: [
        { title: "Click Me" },
        { title: "Click Me" },
        { title: "Click Me" },
        { title: "Click Me 2" }
      ]
    };
  }
};
</script>
