<template>
  <v-dialog max-wdith="600px" v-model="dialog">
    <template v-slot:activator="{ on, attrs }">
      <v-btn text class="success" v-bind="attrs" v-on="on">
        Add new project
      </v-btn>
    </template>
    <v-card>
      <v-card-title class="headline grey lighten-2">
        Dialog
      </v-card-title>
      <v-card-text v-if="shouldNotSubmit">
        <v-alert class="mt-8 mb-0" border="top" color="red lighten-2" dark>
          {{ errorMessage }}
        </v-alert>
      </v-card-text>
      <v-card-text>
        <v-form class="px-3" ref="form">
          <v-text-field
            color="dark"
            label="Title"
            v-model="title"
            prepend-icon="mdi-folder"
            :rules="inputRules"
          ></v-text-field>
          <v-textarea
            color="dark"
            label="Information"
            v-model="content"
            prepend-icon="mdi-lead-pencil"
            :rules="inputRules"
          ></v-textarea>
          <v-menu
            v-model="menu"
            :close-on-content-click="false"
            transition="scale-transition"
            offset-y
            max-width="290px"
            min-width="290px"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                v-model="computedDateFormatted"
                label="Date (read only text field)"
                hint="MM/DD/YYYY format"
                persistent-hint
                prepend-icon="mdi-calendar"
                readonly
                v-bind="attrs"
                v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker
              v-model="date"
              no-title
              @input="menu = false"
            ></v-date-picker>
          </v-menu>
          <v-row row wrap class="text-right">
            <v-col>
              <v-btn
                text
                class="success mx-0 mt-3"
                @click="handleSubmit()"
                :loading="loading"
              >
                Add project
              </v-btn>
            </v-col>
          </v-row>
        </v-form>
      </v-card-text>
      <v-divider></v-divider>
    </v-card>
  </v-dialog>
</template>
<script>
export default {
  name: "ProjectDialog",
  data: vm => ({
    dialog: false,
    title: "",
    content: "",
    menu: false,
    dateFormatted: vm.formatDate(new Date().toISOString().substr(0, 10)),
    date: new Date().toISOString().substr(0, 10),
    inputRules: [
      v => !!v || "Field is required",
      v => (v && v.length >= 3) || "Minimum length is 3"
    ],
    loading: false,
    shouldNotSubmit: false,
    errorMessage: "Please fill form properly .."
  }),
  computed: {
    computedDateFormatted: {
      get() {
        return this.formatDate(
          this.date ? this.date : new Date().toISOString().substr(0, 10)
        );
      },
      set() {
        return new Date().toISOString().substr(0, 10);
        //  this is why we need getter and setter:
        // https://forum.vuejs.org/t/vue/25750
      }
    }
  },
  watch: {
    date() {
      this.dateFormatted = this.formatDate(this.date);
    }
  },
  methods: {
    handleSubmit() {
      this.loading = true;
      if (this.$refs.form.validate()) {
        this.shouldNotSubmit = false;
        console.log(
          "title + content + date",
          this.title,
          this.content,
          this.date
        );
        setTimeout(() => {
          // attributes setup
          this.loading = false;
          this.dialog = false;
          // api call here (POST data)
          // reset
          this.$refs.form.reset();
          this.$refs.form.resetValidation();
          // show snackbar
          this.$emit("projectAdded");
          // close navbar
          this.$emit("closeNavbar");
        }, 3000);
      } else {
        this.loading = false;
        // show hin message
        this.shouldNotSubmit = true;
      }
    },
    formatDate(date) {
      if (!date) return null;
      const [year, month, day] = date.split("-");
      return `${day}/${month}/${year}`;
    },
    parseDate(date) {
      if (!date) return null;
      const [month, day, year] = date.split("/");
      return `${year}-${month.padStart(2, "0")}-${day.padStart(2, "0")}`;
    }
  }
};
</script>
<style scoped></style>
