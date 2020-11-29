<template>
  <v-container>
    <v-layout>
      <v-row>
        <v-col class="inner-container">
          <p class="indigo white--text">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Veritatis
            blanditiis sequi fuga eveniet vero! Temporibus quod rerum, vitae
            porro, porro, quas delectus, consequuntur hic cupiditate sint
            corporis in quidem soluta.
          </p>
          <p class="blue white--text text--darken-8">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Veritatis
            blanditiis sequi fuga eveniet vero! Temporibus quod rerum, vitae
            quas delectus, consequuntur hic cupiditate sint corporis in expedita
            quidem soluta.
          </p>
          <v-divider class="my-4"></v-divider>
          <!-- Typography -->
          <h1 class="display-4">Massive display</h1>
          <h5 class="display-1">Smaller display</h5>
          <p class="headline">Headline text</p>
          <p class="subheading">This is a subheading</p>
          <p class="caption">This is a caption</p>
          <v-divider class="my-4"></v-divider>
          <!-- buttons -->
          <v-btn color="teal white--text" class="mr-2" depressed
            >click me</v-btn
          >
          <v-btn text color="teal" class="mr-2" large>click</v-btn>
          <v-btn depressed color="blue" class="mr-2 white--text" small>
            <v-icon left color="white">mdi-email</v-icon>
            <span>Email Me</span>
          </v-btn>
          <v-divider class="my-4"></v-divider>

          <v-btn fab color="red" small>
            <v-icon color="white">mdi-heart</v-icon>
          </v-btn>

          <v-btn class="hidden-md-and-down">hide when md or sm screen</v-btn>
          <v-btn class="hidden-md-and-up">hide when lg screen</v-btn>
          <v-btn class="hidden-sm-only">hide when only sm screen</v-btn>
          <v-divider class="my-4"></v-divider>
          <!-- Expansion panels -->
          <div>
            <v-expansion-panels>
              <v-expansion-panel v-for="(item, i) in 5" :key="i">
                <v-expansion-panel-header>
                  Item {{ i + 1 }}
                </v-expansion-panel-header>
                <v-expansion-panel-content>
                  Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed
                  eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut
                  ad minim veniam, quis nostrud exercitation ullamco laboris
                  aliquip ex ea commodo consequat.
                </v-expansion-panel-content>
              </v-expansion-panel>
            </v-expansion-panels>
          </div>
          <v-divider class="my-4"></v-divider>
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
          <v-divider class="my-4"></v-divider>
          <!-- watch example -->
          <v-subheader>Watch Example</v-subheader>
          <div>
            <p>Counter by watcher: {{ counter }}</p>
            <v-btn @click="counter++">Counter +</v-btn>
            <v-text-field v-model="someText"></v-text-field>
          </div>
          <v-divider class="my-4"></v-divider>
          <!-- emit from child to parent -->
          <div>
            <p>From child to parent: fire by `$emit`</p>
            <p>Parent view: {{ originaText }}</p>
            <app-playground-child
              :textFromParent="originaText"
              @updateTextContent="originaText = $event"
            />
            <v-card>
              <pre>
                Step 1: parent component -> create a prop called `textFromParent` then bind prop `:textFromParent`
                
                Step 2: parent component -> create a data field called `orignalText` and passed as bind prop to child component
                
                Step 3: child component -> receive the prop from parent component `props: ["textFromParent"]`
                
                Step 4: child component -> bind value prop with child input element `:value="textFromParent"`
                
                Step 5: child component -> create an event for listening child input vlaue change `@input="changeText"`
                
                Step 6: child component -> inside `changeText` method, fire $emit event to trigger child input value change `this.$emit("updateTextContent", this.childText);`
                
                Step 7: parent component -> called this emit event for getting the latest input value and siplay it at parent component `@updateTextContent="originaText = $event"`

                *** Summary: Parent pass prop to child to read, and child emit the event to get the latest updated value for parent to display
              </pre>
            </v-card>
          </div>
          <v-divider class="my-4"></v-divider>
          <!-- dynamic component -->
          <div>
            <!-- eslint-disable-next-line prettier/prettier -->
            <keep-alive>
              <component :is="currentComponent"></component>
            </keep-alive>
            <v-btn @click="currentComponent = 'AppDynamicComponentTwo'">
              Switch To AppDynamicComponentTwo
            </v-btn>
            <v-btn @click="currentComponent = 'AppDynamicComponentOne'">
              Switch To AppDynamicComponentOne
            </v-btn>
            <p class="my-4">
              The most impression on dynamic component: compoennt switcher, eg:
              tab, two forms
            </p>
          </div>
          <v-divider class="my-4"></v-divider>
          <!-- TBD -->
        </v-col>
      </v-row>
    </v-layout>
  </v-container>
</template>
<script>
import DynamicComponentOneVue from "../components/DynamicComponentOne.vue";
import DynamicComponentTwoVue from "../components/DynamicComponentTwo.vue";
import PlaygroundChildVue from "../components/PlaygroundChild.vue";
export default {
  name: "Playground",
  data() {
    return {
      items: [
        { title: "Click Me 1" },
        { title: "Click Me 2" },
        { title: "Click Me 3" },
        { title: "Click Me 4" }
      ],
      counter: 0,
      someText: "",
      originaText: "type here to change text from child to parent ..",
      currentComponent: "AppDynamicComponentOne"
    };
  },
  watch: {
    counter(newVal, oldVal) {
      console.log(`old value ${oldVal}`);
      console.log(`new value ${newVal}`);
    },
    someText: "updateCounter"
  },
  methods: {
    updateCounter() {
      this.counter++;
    }
  },
  components: {
    "app-playground-child": PlaygroundChildVue,
    AppDynamicComponentOne: DynamicComponentOneVue,
    AppDynamicComponentTwo: DynamicComponentTwoVue
  }
};
</script>
<style scoped>
.inner-container {
  max-width: 900px;
  display: block;
  margin: auto;
}
.v-card.v-sheet.theme--light {
  overflow: auto;
  padding-top: 24px;
}
</style>
