<template>
  <div>
    <!-- <v-layout row>
      <v-flex xs12 md6>
        <v-btn outlined block class="blue">1</v-btn>
      </v-flex>
      <v-flex xs12 md6>
        <v-btn outlined block class="blue">2</v-btn>
      </v-flex>
    </v-layout> -->
    <v-container class="my-5">
      <v-row>
        <v-col cols="10" offset="1">
          <v-layout row wrap>
            <v-flex class="d-flex flex-row-reverse">
              <v-tooltip top>
                <template v-slot:activator="{ on, attrs }">
                  <v-btn
                    small
                    text
                    @click="sortByTitle('title')"
                    class="mx-3"
                    v-bind="attrs"
                    v-on="on"
                    >Sort by title</v-btn
                  >
                </template>
                <span class="caption text-lowercase">Filter by title</span>
              </v-tooltip>
              <v-tooltip top>
                <template v-slot:activator="{ on, attrs }">
                  <v-btn
                    small
                    text
                    @click="sortByTitle('person')"
                    v-bind="attrs"
                    v-on="on"
                    >Sort by person</v-btn
                  >
                </template>
                <span class="caption text-lowercase">Filter by person</span>
              </v-tooltip>
            </v-flex>
          </v-layout>
          <!-- <v-expansion-panels>
            <v-expansion-panel v-for="project in projects" :key="project.title">
              <v-expansion-panel-header>
                <v-layout
                  row
                  wrap
                  :class="`ml-0 mt-1 pa-4 project ${project.status}`"
                >
                  <v-flex xs12 md6>
                    <div class="caption grey--text">Project title</div>
                    <div>{{ project.title }}</div>
                  </v-flex>
                  <v-flex xs6 sm4 md2>
                    <div class="caption grey--text">Person</div>
                    <div>{{ project.person }}</div>
                  </v-flex>
                  <v-flex xs6 sm4 md2>
                    <div class="caption grey--text">Due by</div>
                    <div>{{ project.due }}</div>
                  </v-flex>
                  <v-flex xs6 sm4 md2>
                    <div class="caption grey--text">Status</div>
                    <v-chip :class="`${project.status}`">{{
                      project.status
                    }}</v-chip>
                  </v-flex>
                </v-layout>
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                {{ project.content }}
              </v-expansion-panel-content>
            </v-expansion-panel>
          </v-expansion-panels> -->
          <v-card flat v-for="project in projects" :key="project.title">
            <v-layout
              row
              wrap
              :class="`ml-0 mt-1 pa-4 project ${project.status}`"
            >
              <v-flex xs12 md6>
                <div class="caption grey--text">Project title</div>
                <div>{{ project.title }}</div>
              </v-flex>
              <v-flex xs6 sm4 md2>
                <div class="caption grey--text">Person</div>
                <div>{{ project.person }}</div>
              </v-flex>
              <v-flex xs6 sm4 md2>
                <div class="caption grey--text">Due by</div>
                <div>{{ project.due }}</div>
              </v-flex>
              <v-flex xs6 sm4 md2>
                <div class="caption grey--text">Status</div>
                <v-chip :class="`${project.status}`">{{
                  project.status
                }}</v-chip>
              </v-flex>
            </v-layout>
            <v-divider></v-divider>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      projects: [
        {
          title: "Design a new website",
          person: "The Net Ninja",
          due: "1st Jan 2019",
          status: "ongoing",
          content:
            "Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!"
        },
        {
          title: "Code up the homepage",
          person: "Chun Li",
          due: "10th Jan 2019",
          status: "complete",
          content:
            "Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!"
        },
        {
          title: "Design video thumbnails",
          person: "Ryu",
          due: "20th Dec 2018",
          status: "complete",
          content:
            "Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!"
        },
        {
          title: "Create a community forum",
          person: "Gouken",
          due: "20th Oct 2018",
          status: "overdue",
          content:
            "Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!"
        }
      ]
    };
  },
  methods: {
    sortByTitle(prop) {
      this.projects.sort((a, b) => (a[prop] < b[prop] ? -1 : 1));
    }
  }
};
</script>
<style scoped>
.project.complete {
  border-left: 4px solid #3cd1c2;
}
.project.ongoing {
  border-left: 4px solid orange;
}
.project.overdue {
  border-left: 4px solid tomato;
}
/* replace colors with vuetify built-in classes */
.theme--light.v-chip.complete {
  background: #3cd1c2;
}
.theme--light.v-chip.ongoing {
  background: orange;
}
.theme--light.v-chip.overdue {
  background: tomato;
}
</style>
