<template>
  <div class="about">
    <v-container class="my-5">
      <v-layout row wrap v-if="team && team.length > 0">
        <v-flex xs12 sm6 md4 lg3 v-for="person in team" :key="person.name">
          <v-card flat class="ma-3">
            <v-responsive class="pt-4 subtitle-2 text-center">
              <v-avatar size="80" class="grey">
                <img :src="person.avator" :alt="person.name" />
              </v-avatar>
            </v-responsive>
            <v-card-text>
              <div class="subheading">{{ person.name }}</div>
              <div class="grey--text">{{ person.role }}</div>
            </v-card-text>
            <v-card-actions>
              <v-btn text color="grey">
                <v-icon small left>mdi-message</v-icon>
                <span>Message</span>
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
export default {
  name: "About",
  data() {
    return {
      team: [
        { name: "The Net Ninja", role: "Web developer", avator: "/" },
        { name: "Ryu", role: "Graphic designer", avator: "/" },
        { name: "Chun Li", role: "Web developer", avator: "/" },
        { name: "Gouken", role: "Social media maverick", avator: "/" },
        { name: "Yoshi", role: "Sales guru", avator: "/" }
      ]
    };
  }
};
</script>
